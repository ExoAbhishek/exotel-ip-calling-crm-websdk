# ExotelCRMWebSDK (Beta)


The ExotelCRMWebSDK allows you to leverage Exotel's platform for making IP calls, with this easy to integrate feature.

## Installation

You can install the package using npm:

```bash
npm install git+https://github.com/exotel/exotel-ip-calling-crm-websdk#v1.1.1
```

## Using the Package in a Project:

Refer to sample project [here](https://github.com/exotel/exotel-voip-websdk-crm-sample-app) or read on.

1. Simply import the ExotelCRMWebSDK in your code like this:
```js
import ExotelCRMWebSDK from "exotel-ip-calling-crm-websdk";
```

2. Configure crmWebSDK object like this:
```js
const crmWebSDK = new ExotelCRMWebSDK(accessToken, userId, true);
```

3. **ExotelCRMWebSDK**
    
    **contructor**
      
      **accessToken** : This can be generated using the 
  [Create Authentication Token API](https://developer.exotel.com/api/ip-pstn-intermix-webrtc-sdk-integration#create-authentication-token)

    **userId** : You can get the userId using the [Application user management APIs](https://developer.exotel.com/api/ip-pstn-intermix-webrtc-sdk-integration#applications-user-management)
    
    **autoConnectVOIP** : If true, it will auto-connect device when the `ExotelWebPhoneSDK` is returned on initialization. (If you have passed false, then you must call `DoRegister` on `ExotelWebPhoneSDK`)

    **Initialize**

    Initializes the CRMWebSDK, sets up the phone object, and registers callbacks for various events.

    Parameters:

    `sofPhoneListenerCallback` (function): Callback for incoming calls.
    
    `softPhoneRegisterEventCallBack` (function, optional): Callback for soft phone register events. Default is null.
    
    `softPhoneSessionCallback` (function, optional): Callback for soft phone session events. Default is null.

    Returns:

    Promise<ExotelWebPhoneSDK | void>: A promise that resolves to an instance of ExotelWebPhoneSDK if successful, or void if unsuccessful.
 
4. Use the `Initialize` method on the `ExotelCRMWebSDK` object which returns Promise that resolves to `ExotelWebPhoneSDK` object.
    `ExotelCRMWebSDK` does all the work to get necessary details required for the `ExotelWebPhoneSDK`

```javascript
const crmWebPhone = await crmWebSDK.Initialize(HandleCallEvents, RegisterationEvent);
```

You must pass call events handler, registeration event handler (optional) and session callback handler (optional) to the `Initialize` method

5. **ExotelWebPhoneSDK**
   
   1. **RegisterDevice**: Registers the device with the call server.
   2. **UnRegisterDevice**: Un-registers the device from the call server.
   3. **AcceptCall**: Accept call
   4. **HangupCall**: Disconnect call
   5. **MakeCall**: (async) Method that places a call
        
        **Number**: A number to dial

        **dialCallback**: It is called after the call request is made to the server (An actual call may start after this with a slight day).

        **CustomField**: String; Any application-specific value like order id that will be passed back as a parameter in status callback.

   7. **ToggleHold**: Toggle state hold/un-hold state of a call. This state needs to be maintained by the client
   8. **ToggleMute** Toggle state mute/un-mute state of a call. This state needs to be maintained by the client

## License

This project is licensed under the Apache-2.0 License. See the [LICENSE](https://apache.org/licenses/LICENSE-2.0) file for details.
