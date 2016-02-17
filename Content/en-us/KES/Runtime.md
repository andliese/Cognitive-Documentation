# Command Line Interface
The IRIS command line interface provides the ability to build index and grammar files from structured data and deploy them as web services.  It uses the general syntax: `iris.exe <command> <required_args> [<optional_args>]`.  You can run `iris.exe` without arguments to display a list of commands or `iris.exe <command>` to display a list of arguments available for the specified command.  Below is a list of available commands:
* build_index
* build_grammar
* host_service
* deploy_service
* describe_index
* describe_grammar

## build_index Command
The **build_index** command builds a binary index file from a schema definition file and data file of objects to index.  The resulting index file can be used to evaluate structured query expressions, or generate interpretations of natural language queries in conjunction with a compiled grammar file.

`iris.exe build_index <schemaFile> <dataFile> <indexFile> [options]`

| Parameter      | Description               |
|----------------|---------------------------|
| `<schemaFile>` | Input schema path |
| `<dataFile>`   | Input data path   |
| `<indexFile>`  | Output index path |
| `--description <description>` | Description string |
| `--remote <vmSize>`           | Size of VM for remote build |

Schema/data/index files may be local file paths or URL paths to Azure blobs.  The schema file describes the structure of the objects being indexed as well as the operations to support (see [Schema Format]()).  The data file enumerates the objects and attribute values to index (see [Data Format]()).  When the build succeeds, the output index file contains a compressed representation of the input data that support the desired operations.  

A description string may be optionally specified to subsequently identify a binary index using the **describe_index** command.  

By default, the index is built on the local machine.  Outside of the Azure environment, local builds are limited to data files up to 1 MB in size.  When the --remote flag is specified, the index will be built on a dynamically created Azure VM of the specified size.  This allows large indices to be built efficiently using Azure VMs with more memory.  To avoid paging which slows down the build process, we recommend using a VM with 3 times the amount of RAM as the input data file size.  For a list of available VM sizes, see [Sizes for virtual machines](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-size-specs/).

TIP: For faster builds, presort the objects to index from the data file by decreasing probability.

To Do:
* Need to describe how to download subscription information.  If the command allows this to be specified interactively, we don't have to document.
* Do we want to document that indexFile has to be blob if remote.
* For now, remote build requires indexFile to be a blob.

## build_grammar Command
The **build_grammar** command compiles a grammar specification in XML format to a binary grammar file.  The resulting grammar file can be used in conjunction with an index file to generate interpretations of natural language queries.

`iris.exe build_grammar <xmlFile> <grammarFile>`

| Parameter       | Description               |
|-----------------|---------------------------|
| `<xmlFile>`     | Input XML grammar specification path |
| `<grammarFile>` | Output compiled grammar path         |

XML/grammar files may be local file paths or URL paths to Azure blobs.  The grammar specification describes the set of weighted natural language expressions and their semantic interpretation (see [Grammar Format]()).  When the build succeeds, the output grammar file contains a binary representation of the grammar specification to enable fast decoding.

## host_service Command
The **host_service** command hosts an instance of the IRIS service on the local machine.

`iris.exe host_service <grammarFile> <indexFile> [options]`

| Parameter       | Description                |
|-----------------|----------------------------|
| `<grammarFile>` | Input grammar path         |
| `<indexFile>`   | Input index path           |
| `--port <port>` | Local port.  Default: 8000 |

Index/grammar files may be local file paths or URL paths to Azure blobs.  A web service will be hosted at http://localhost:&lt;port&gt;/.  See [Service APIs]() for a list of supported operations.

Outside of the Azure environment, locally hosted services are limited to index files up to 1 MB in size, 1 request per second, and 1000 total calls.  To overcome this limitation, run **host_service** inside an Azure VM or deploy to an Azure cloud service using **deploy_service**.

## deploy_service Command
The **deploy_service** command deploys an instance of the IRIS service to an Azure cloud service.

`iris.exe deploy_service <grammarFile> <indexFile> <serviceName> <vmSize>[options]`

| Parameter       | Description                  |
|-----------------|------------------------------|
| `<grammarFile>` | Input grammar path           |
| `<indexFile>`   | Input index path             |
| `<serviceName>` | Name of target cloud service |
| `<vmSize>`      | Size of cloud service VM     |
| `--slot <slot>` | Cloud service slot: "staging" (default), "production" |

Index/grammar files must be URL paths to Azure blobs.  Service name specifies  a preconfigured Azure cloud service (see [How to Create and Deploy a Cloud Service](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-how-to-create-deploy/)).  The command will automatically deploy the IRIS service to the specified Azure cloud service, using VMs of the specified size.  To avoid paging which significantly decreases performance, we recommend using a VM with 1 GB more RAM than the input index file size.  For a list of available VM sizes, see [Sizes for Cloud Services](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-sizes-specs/).

By default, the service is deployed to the staging environment, optionally overridden via the --slot parameter.  See [Service APIs]() for a list of supported operations.

## describe_index command
The **describe_index** command outputs information about an index file, including the build timestamp, schema, and description.

`iris.exe describe_index <indexFile>`

| Parameter     | Description      |
|---------------|------------------|
| `<indexFile>` | Input index path |

Index file may be local file path or a URL path to an Azure blob.  The output description string can be specified using the --description parameter of the **build_index** command.

## describe_grammar command
The **describe_grammar** command outputs the original grammar specification used to build the binary grammar.

`iris.exe describe_grammar <grammarFile>`

| Parameter       | Description      |
|-----------------|------------------|
| `<grammarFile>` | Input grammar path |

Grammar file may be local file path or a URL path to an Azure blob.





# To Do
* Change max string attribute value length to 4096.  Error if exceeded.  Error if empty value.
* Copy files from local file system to VM without intermediate storage blob.
  * https://www.veeam.com/fastscp-azure-vm.html
  * https://gallery.technet.microsoft.com/scriptcenter/Copy-a-File-to-an-Azure-VM-d2ad9e1f
  * https://gallery.technet.microsoft.com/scriptcenter/Copy-and-Item-from-an-c283405d
* Create VM without storage account.
  * https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-command-line-tools/#commands-to-manage-your-azure-virtual-machines
  * `azure vm create my-vm-name MSFT__Windows-Server-2008-R2-SP1.11-29-2011 username --location "West US"`

  * Document that user needs to pre-config an Azure Cloud Service before running host command
* If we download files from blob, do we remove them afterwards?
* Verify that if schema between grammar and index mismatches, we throw or work if compatible.
* Reverse grammar/index positional parameters.  Need to update code to reflect.



* Use the style and examples from [Azure command line tool](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-command-line-tools/#commands-to-manage-your-azure-virtual-machines) to design our command line interface.