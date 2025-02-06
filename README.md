# Webflow API Connector for Power Automate

This repository contains an OpenAPI (Swagger 2.0) definition for a custom connector that integrates with the Webflow API (v2). This custom connector allows you to create, retrieve, and update CMS items in a Webflow collection directly from Power Automate.

> **Important:** Webflow is sunsetting its Logic functionality soon. This custom connector offers a robust alternative to automate your Webflow CMS operations via direct API calls in Power Automate.

---

## Features

- **Create CMS Item:**  
  Create a new CMS item in a Webflow collection by sending a JSON payload with required fields (`slug` and `name`) and optional fields such as `run-count`.

- **Get CMS Items:**  
  Retrieve all CMS items from a collection, with optional pagination parameters (`limit` and `offset`).

- **Get CMS Item:**  
  Retrieve a specific CMS item by its unique ID.

- **Update CMS Item Run Count:**  
  Update an existing CMS item (for example, modifying the `run-count` value) using a PATCH request. Note that when updating, the API requires that you also supply the required fields (`slug` and `name`).

---

## Prerequisites

- **Webflow API Token:**  
  Obtain a valid API token from your Webflow dashboard. When using this connector, supply your token with the prefix `Bearer ` (e.g., `Bearer YOUR_WEBFLOW_API_TOKEN`).

- **CMS Collection ID:**  
  Know the collection ID where you want to manage CMS items.

- **Microsoft Power Automate Account:**  
  You will need a Power Automate account to import and use this custom connector.

---

## Installation

1. **Download the YAML File:**  
   Clone this repository or download the `webflow-connector.yaml` file from the repository.

2. **Import into Power Automate:**
   - Open Power Automate.
   - Navigate to **Data** > **Custom Connectors** > **New custom connector** > **Import an OpenAPI file**.
   - Upload the `webflow-connector.yaml` file.
   - Under the **Security** tab, select **API key** as the authentication type.
   - Enter your Webflow API token (remember to prefix it with `Bearer `).

3. **Save and Test:**  
   After importing, create a test flow to verify that each operation (create, retrieve, update) works as expected.

---

## API Endpoints

### Create CMS Item

- **Endpoint:**  
  `POST /v2/collections/{collectionId}/items`

- **Description:**  
  Creates a new CMS item in a specified Webflow collection.

- **Request Body Example:**

  ```json
  {
    "items": [
      {
        "fieldData": {
          "slug": "qb-flow",
          "name": "qb-flow",
          "run-count": 25,
          "_archived": false,
          "_draft": false
        }
      }
    ]
  }
  ```

---

### Get CMS Items

- **Endpoint:**  
  `GET /v2/collections/{collectionId}/items`

- **Description:**  
  Retrieves all CMS items in the specified collection.

- **Optional Query Parameters:**  
  - `limit`: Maximum number of items to return.
  - `offset`: Offset for pagination.

---

### Get a CMS Item

- **Endpoint:**  
  `GET /v2/collections/{collectionId}/items/{itemId}`

- **Description:**  
  Retrieves a single CMS item by its unique ID.

---

### Update CMS Item Run Count

- **Endpoint:**  
  `PATCH /v2/collections/{collectionId}/items/{itemId}`

- **Description:**  
  Updates an existing CMS item. The payload must include the required fields (`slug` and `name`) along with the field you wish to update (e.g., `run-count`).

- **Request Body Example:**

  ```json
  {
    "fields": {
      "slug": "qb-flow",
      "name": "qb-flow",
      "run-count": 30,
      "_archived": false,
      "_draft": false
    }
  }
  ```

---

## Using the Connector in Power Automate

After importing the connector:

- **Creating an Item:**  
  Use the **createCMSItem** operation and provide the collection ID along with a JSON payload (as shown in the example above).

- **Retrieving Items:**  
  Use the **getCMSItems** and **getCMSItem** operations to list or fetch specific CMS items from your collection.

- **Updating an Item:**  
  Use the **updateCMSItemRunCount** operation to update the run count (or other fields) for an existing CMS item.

---

## Contributing

Contributions, issues, and feature requests are welcome! If you have suggestions or improvements, please open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Disclaimer

This custom connector is provided "as is" without any warranty. Use it at your own risk. The maintainers are not responsible for any issues that arise from its use in production.

---

Happy automating! If you have any questions or need further assistance, feel free to reach out on our GitHub issues page or join the community discussions.
