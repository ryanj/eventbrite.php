#PHP Eventbrite API Client Library
----------------------------------

##  WARNING: This library uses Eventbrite API endpoints that have been deprecated (as of April 2015). 
See Eventbrite's developer site for updated info on how to use thier new APIs: https://developer.eventbrite.com

## Requirements: ##
### API key ###
Eventbrite API keys are available here: http://www.eventbrite.com/api/key/
### User key ###
Eventbrite User_keys are optional.  They are only required if you need to access private data.  Eventbrite users can find their user_key here: 
http://www.eventbrite.com/userkeyapi

# Examples: #
### Load the API Client library ###

    require 'Eventbrite.php';

### Initialize the client by setting your authentication tokens ###
Add your authentication tokens to make this example work:

    $eb_client = new Eventbrite( array('app_key'=>'YOUR_APP_KEY', 
                                       'user_key'=>'YOUR_USER_KEY'));

### Initialization using OAuth2.0 tokens ###
You can also initialize the API client with an OAuth2.0 "access_token":

    $eb_client = new Eventbrite( array('access_token'=>'YOUR_ACCESS_TOKEN')); 

Or, initialize the client by using an intermediary OAuth2.0 "access_code", which will automaticaly be exchanged for an OAuth2.0 "access_token":

    $eb_client = new Eventbrite(array('app_key'=>'YOUR_API_KEY', 
                                      'client_secret'=>'YOUR_CLIENT_SECRET',
                                      'access_code'=>'YOUR_ACCESS_CODE' )); 

For more information and usage examples regarding OAuth2.0, see our [OAUTH2-README.md](https://github.com/ryanjarvinen/eventbrite.php/blob/master/OAUTH2-README.md)

## Documentented API methods will be available on the client object ##
See Eventbrite's [API Docs](http://developer.eventbrite.com/doc) for more information about the available method calls.  Request parameters should be encapsulated in an array of key/value pairs as in the examples below:

### event_get example ###

    // request an event by adding a valid EVENT_ID value here:
	$resp = $eb_client->event_get( array('id' => 'EVENT_ID') );

    // print a ticket widget for the event:
    print( Eventbrite::ticketWidget($resp->event) );

### event_search example ###

    $search_params = array(
        'max' => 2,
        'city' => 'San Francisco',
        'region' => 'CA',
        'country' => 'US'
    );
	$resp = $eb_client->event_search( $search_params );

### event_new example ###

    $new_event_params = array(
        'title' => 'My test event',
        'description' => 'testing event creation, remember not to set the privacy or visibility of test events to "public".',
        'start_date' => date('Y-m-d H:i:s', time() + (7 * 24 * 60 * 60)),
        'end_date' => date('Y-m-d H:i:s', time() + (7 * 24 * 60 * 60) + (2 * 60 * 60) )
    );
    try{
        $response = $eb_client->event_new($new_event_params);
    }catch( Exception $e ){
        // application-specific error handling goes here
        $response = $e->error;
    }

### Rendering lists of events as HTML ###
If you are planning to use PHP to help keep your site's event listing up to date, take a look at this guide: [https://github.com/ryanjarvinen/eventbrite.php/blob/master/examples/event-list-example.md](https://github.com/ryanjarvinen/eventbrite.php/blob/master/examples/event-list-example.md)

## More information about available API methods
Eventbrite API documentation:  http://developer.eventbrite.com/doc

# Resources: #
* <a href="http://eventbrite.github.com/">Eventbrite on GitHub</a>
* <a href="http://developer.eventbrite.com/doc/">API Documentation</a>
* <a href="http://developer.eventbrite.com/doc/getting-started/">API Getting-Started Guide</a>
* <a href="http://developer.eventbrite.com/terms/">Eventbrite API terms and usage limitations</a>
* <a href="http://developer.eventbrite.com/news/branding/">Eventbrite Branding Guidelines</a>
