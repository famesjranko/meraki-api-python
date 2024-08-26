# Meraki Camera MQTT Broker Reset Script

This Flask-based web application resets the MQTT broker settings for specified Meraki MV cameras. The script ensures that each camera's MQTT broker is correctly configured by updating any cameras that have incorrect settings. The application provides a web interface to run the update script and returns a summary of the camera configurations.

## Features

- Retrieves the current MQTT broker settings for Meraki MV cameras.
- Updates MQTT broker settings for specified cameras if they are not configured correctly.
- Provides a web interface to trigger the update and view the status of all cameras.
- Generates a summary of the camera configurations, including their current MQTT broker ID and topics.

## Prerequisites

- Python 3.6 or higher
- Flask
- Meraki Dashboard API Python SDK

## Installation

1. Clone the repository:

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

3. Set your Meraki API key:

    You can set your API key either in the script directly (`API_KEY` variable) or by setting it as an environment variable:

    ```bash
    export MERAKI_DASHBOARD_API_KEY=<your_api_key>
    ```

4. Configure the organization ID, network ID, and MQTT broker ID in the script according to your setup.

## Usage

1. Start the Flask web server:

    ```bash
    python app.py
    ```

2. Access the web interface:

    Open your browser and navigate to [http://localhost:5000](http://localhost:5000).

3. Trigger the MQTT broker update by clicking the "Run Script" button on the interface.

4. The script will scan all Meraki MV cameras in the specified network and update their MQTT broker settings if needed.

## Configuration

- **API Key:** Set your Meraki API key via the `API_KEY` variable or as an environment variable.
- **Organization and Network IDs:** Set the organization and network IDs based on your Meraki setup.
- **MQTT Broker ID:** Define the correct MQTT broker ID that should be set on your cameras.
- **MAC Addresses:** The script only updates the cameras specified in the `mac_addresses_to_update` list.

## API Endpoints

- **GET /:** Returns the web interface.
- **POST /run-script:** Runs the update script and returns a JSON summary of camera configurations.

## Example Summary Output

The output from running the script includes:

```json
{
    "summary": [
        {
            "name": "CollaborationHub201C",
            "serial": "Q2DY-HAUC-J77B",
            "mac": "0c:7b:c8:da:a6:52",
            "updated": true,
            "mqtt_broker_id": "833165931063541914",
            "topics": []
        },
        ...
    ]
}
```
## Notes

The script adds a delay of 5 seconds after updating each camera to ensure the changes take effect.
The Flask app runs on port 5000 by default. You can adjust this in the app.run() call if needed.

# Retrieving Meraki API Key, Organization ID, Network ID, and MQTT Broker ID

This guide explains how to obtain the necessary details to configure the Meraki MQTT broker reset script.

## 1. Getting the Meraki API Key

Your Meraki API key is required to authenticate with the Meraki Dashboard API.

1. Log in to your Meraki Dashboard at [dashboard.meraki.com](https://dashboard.meraki.com).
2. Click on your account profile in the upper-right corner and select **My Profile**.
3. Scroll down to the **API Access** section.
4. If you don’t have an API key yet, click on **Generate new API key**. Your key will be displayed once generated. **Be sure to copy and store this key securely**, as it won't be shown again.
5. Set the API key in your environment using the following command (recommended for security):

    ```bash
    export MERAKI_DASHBOARD_API_KEY=<your_api_key>
    ```

Alternatively, you can directly set it in the script by modifying the `API_KEY` variable:

```python
API_KEY = '<your_api_key>'
```

## 2. Finding Your Organization ID
The organization ID is needed to identify the Meraki organization you want to work with.

1. Log in to the Meraki Dashboard.

2. In the URL, you'll see something like:

```bash
https://dashboard.meraki.com/o/<organization_id>/manage/organization/overview
```
3. The value after /o/ is your organization ID. Copy this value.

4. Set the organization_id variable in the script:

```python
organization_id = '<your_organization_id>'
```

## 3. Finding Your Network ID
The network ID is specific to the network where your Meraki devices are located.

1. In the Meraki Dashboard, navigate to Networks > Network List.

2. Select the network you want to configure.

3. In the URL, you’ll see something like:

```bash
https://dashboard.meraki.com/n/<network_id>/manage/overview
```
4. The value after /n/ is your network ID. Copy this value.

5. Set the network_id variable in the script:

```python
network_id = '<your_network_id>'
```

## 4. Finding Your MQTT Broker ID
The MQTT broker ID is associated with the MQTT broker you want to configure for your cameras.

1. Log in to the Meraki Dashboard and go to Network-wide > Settings > MQTT.

2. If you have already configured a broker, you will see it listed along with its MQTT broker ID.

3. Note down the MQTT broker ID.

4. Set the mqtt_broker_id variable in the script:

```python
mqtt_broker_id = '<your_mqtt_broker_id>'
```

## Summary
Once you have retrieved all the required IDs and the API key, you can set them in your script or as environment variables. Here’s an example of the final configuration in your script:

```python
API_KEY = '<your_api_key>'
organization_id = '<your_organization_id>'
network_id = '<your_network_id>'
mqtt_broker_id = '<your_mqtt_broker_id>'
```

You’re now ready to run the script with the correct settings for your Meraki cameras.
