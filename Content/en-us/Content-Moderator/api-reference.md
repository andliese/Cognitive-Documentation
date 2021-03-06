<!-- 
NavPath: Content Moderator
LinkLabel: API Reference
Url: content-moderator/documentation/api-reference
Weight: 130
-->

# API Reference #

## Review API ##
When you sign up for the [human review tool](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool"), you can use the credentials available within the review tool, to call teh review API and integrate your content in bulk. The review API will internally use the image or text moderation APIs to scan your content and create reviews in the online tool for human moderation.

[**Review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5 "Content Moderator Review API")

## Image and Text Moderation APIs ##
Get started by either [subscribing to the Content Moderator API](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/ContentModerator) on the Azure portal or by signing up for the online [review tool](http://contentmoderator.cognitive.microsoft.com/). In the latter case, you will find your content moderator API credentials listed on the Settings screen in the review tool.

The image and text moderation APIs scan your content and send the results with relevant information either back to your systems or to the built-in review tool, depending on who is calling the API. You can use this information to implement your own post-moderation workflow such as publish, reject, or review.

[**Image and Text Moderation APIs**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c "Image and Text Moderation APIs")

## List Management API ##
You can use your Content Moderator API credentials (for image, text and reviews) for the list management API as well. Use this API to create and manage your custom lists of Images and Text. The lists that you create can be used in the **Image/Match** and **Text/Screen** operations. 

[**List Management API**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator List Management API")
