Installation

You can install this package via npm:

npm i react-native-get-post-request

Features

    •	Flexible API Requests: Fetch and post data with optional headers, payloads, and certificates.
    •	Loading State Management: Automatically manages loading states for both GET and POST requests.
    •	Error Handling: Handle errors efficiently during API interactions.
    •	Data Transformation: Customize how the data is processed upon fetching or posting.
    •	Secure API Requests: Supports optional certificate validation for secure connections.
    •	Activity Indicators: Provides feedback while loading, with customizable indicators.

Example: Usage with useGetDataFromServer and usePostDataToServer

Below is a React Native component showcasing both GET and POST requests, secure certificate handling, and custom UI interactions.

#### Example

```javascript

import React from 'react';
import {
ActivityIndicator,
Platform,
StyleSheet,
Text,
View,
} from 'react-native';
import {
usePostDataToServer,
useGetDataFromServer,
} from 'react-native-get-post-request';

const certificateObject = {
live_certs: [...], // Certificates sha keys for secure environment
};

function App(): React.JSX.Element {
const { data, isLoading, isError, postData } = usePostDataToServer();

const handlePostFetch = () => {
postData({
API_URL: 'url',
structureApiData: (data) => data,
onPostReqSuccess: (finalData) => console.log('Success:', finalData),
onError: (error) => console.error('Error:', error),
secure: true,
certificate: certificateObject,
});
};

return (
<View style={styles.container}>
<Text style={styles.buttonColor} onPress={handlePostFetch}>
Button
</Text>
{isLoading && (
<View style={styles.loadingOverlay}>
<ActivityIndicator
color={'white'}
size={Platform.OS === 'android' ? 100 : 'large'}
/>
</View>
)}
</View>
);
}

const styles = StyleSheet.create({
container: {
flex: 1,
justifyContent: 'center',
alignItems: 'center',
backgroundColor: 'lightblue',
},
buttonColor: {
fontSize: 30,
backgroundColor: 'red',
padding: 20,
color: 'white',
},
loadingOverlay: {
position: 'absolute',
height: 1000,
width: 1000,
justifyContent: 'center',
alignContent: 'center',
backgroundColor: 'black',
opacity: 0.5,
},
});

export default App;

```

# Hook Parameters `(GET) and (POST)`

    •	API_URL (string): The URL of the API endpoint.
    •	HEADERS (object, optional): Custom headers for the API request (default: {}).
    •	body (object, optional for POST): Data to be sent with POST requests.
    •	secure (boolean, optional): Indicates whether to enforce certificate-based security.
    •	certificate (object, optional): A certificate object for SSL validation.
    •	onPostReqSuccess / onGetReqSuccess (function, optional): Callbacks for successful requests.
    •	onError (function, optional): Callback for handling errors.

### Return Values `(GET) and (POST)`

    •	data: The fetched or posted data from the server.
    •	isLoading: A boolean indicating if the request is in progress.
    •	isError: A boolean indicating if an error occurred.

### License

```
This project is licensed under the ISC License.
```
