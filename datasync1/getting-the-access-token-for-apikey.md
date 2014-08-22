---
title: Getting the Access Token for ApiKey
page_title: DataSync Getting the Access Token for ApiKey
position: 4
---

# DataSync: Getting the Access Token for ApiKey

Telerik DataSync for iOS requires an access token string value in order be able to communicate with Telerik Backend Services. This access token is unique for all application users and should be acquired by a specific url request as it is described below. In order to prepare the request, we need the ApiKey that is unique for Backend Services application.

The following snippets demonstrate how to prepare this request and process the response. The given code snippets execute a synchronous call just for the simplicity of the example. If you need an asynchronous call, you may use any of the available async approaches for URL requests/response handling like, for example, the implementation of the NSURLConnectionDelegate together with running the NSURLConnection, wrapping everything in an NSOperation instance or use GCD appropriately.

Let us now define a property for required access token:


@property (nonatomic, strong) NSString* accessToken;


Then we can lazy load it in getter:


-(NSString*) accessToken{
    if (_accessToken) {
        return _accessToken;
    }

    [self obtainAccessTokenForApiKey:@"bdRwVIeRfgZpsJyTcPR"]; //Use your ApiKey as parameter
    return _accessToken;
}


Now we will define a method that will get the access token synchronously. You can reuse this code for asynchronous approaches, skipping the sendSyncrhonousRequest: call of course:

-(void)obtainAccessTokenForApiKey:(NSString*) apiKey
{
    //Use appropriate username & password here
    NSDictionary* userInfo= @{  @"username": @"andy", @"password": @"1", @"grant_type": @"password"};
    NSError *error;
    NSData* body  = [NSJSONSerialization dataWithJSONObject:userInfo
                                                    options:NSJSONWritingPrettyPrinted
                                                      error:&error];

    NSString* strUrl = [NSString stringWithFormat:@"http://api.everlive.com/v1/%@/oauth/token", apiKey];
    NSURL* url = [NSURL URLWithString:strUrl];

    NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:url
                                                          cachePolicy:NSURLRequestReloadIgnoringLocalCacheData
                                                       timeoutInterval:30];

    [request setHTTPMethod:@"POST"];
    [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
    [request setHTTPBody:body];

    NSURLResponse* response = nil;
    NSData* data = [NSURLConnection sendSynchronousRequest:request returningResponse:&response error:&error];

    NSDictionary *res = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingMutableLeaves error:&error];

    // show all values , just for debug purposes
    for(id key in res){
        id value = [res objectForKey:key];

        NSString *strKey = (NSString *)key;
        NSString *strValue = (NSString *)value;
        NSLog(@"key: %@ \nvalue: %@", strKey, strValue);
    }

    // extract access token value only
    NSDictionary* resDict = [res objectForKey:@"Result"];
    NSString *token = [resDict objectForKey:@"access_token"];
    NSLog(@"Access token: %@", token);

    _accessToken = token;
}
