
Reporting a possible bug on Youtube Api commentThreads.update 

This is the official topic:
https://code.google.com/p/gdata-issues/issues/detail?id=8729


Name of API affected: CommentThreads: update


Issue summary:
CommentThreads: update 
When calling this api to update the topLevelComment returned by CommentThreads.list, I got a 400 error.
I was using this API in an internal tool to allow me respond to comments. I was working fine for the last months... and in the last days (~2016-11-07) with no changes on any code on my side, the API started to return a 400 error. I have all my internal comment systems halted right now as I could not figure out how to fix this. Every thing I tried and tested brings me to the 400 error and the message below.

"While this can be a transient error, it usually indicates that the requests input is invalid."

My bet? This is a transient error that I hope Google can fix. 


Steps to reproduce issue:
1. Retrieve "heldForReview" threads using CommentThreads.list
2. Try to update the returned topLevelComment changing ["topLevelComment"]["snippet"]["textOriginal"] = "some text". Optionally, change the "moderationStatus" to "published". The error is the same.
3. This behaviour can be easily spotted using the Python API samples, specifically the file comment_threads.py from https://github.com/youtube/api-samples/blob/master/python/comment_threads.py

Expected output:
The top level comment from Thread should become visible (after setting the moderationStatus to published) and have the "some text" as the first child comment as its answer.

Actual results:
An HTTP error 400 occurred:
{
 "error": {
  "errors": [
   {
    "domain": "youtube.commentThread",
    "reason": "processingFailure",
    "message": "The API server failed to successfully process the request. While this can be a transient error, it usually indicates that the requests input is invalid. Check the structure of the \u003ccode\u003ecommentThread\u003c/code\u003e resource in the request body to ensure that it is valid.",
    "locationType": "other",
    "location": "body"
   }
  ],
  "code": 400,
  "message": "The API server failed to successfully process the request. While this can be a transient error, it usually indicates that the requests input is invalid. Check the structure of the \u003ccode\u003ecommentThread\u003c/code\u003e resource in the request body to ensure that it is valid."
 }
}


Notes:
I am providing a sample code above. I just changed one line of https://github.com/youtube/api-samples/blob/master/python/comment_threads.py to only list "heldForReview" comments.
I also removed the the "insert_comment" calls to insert channel comments.
You can see all changes to the default sample code in this commit:
https://github.com/alexbenfica/commentThreads.update-bug-report/commit/65c8b26f7e63faa91d2f4d8e0f964caaa7074ba8


Sample code here:
https://github.com/alexbenfica/commentThreads.update-bug-report/


Of course, you will need your authorization files.




