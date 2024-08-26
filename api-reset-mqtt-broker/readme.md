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
