# Similarix: Semantic and Multimodal Search Client

![PyPI version](https://img.shields.io/pypi/v/similarix.svg)
![Python versions](https://img.shields.io/pypi/pyversions/similarix.svg)

Similarix is a Python client for interacting with the [Similarix API](https://similarix.com/docs/), enabling semantic and multimodal search capabilities for both images and text.  

This client can integrate with S3 compatible storage, adding an AI layer to enhance searchability and organization of digital assets. It addresses S3's lack of native search functionality.

For those who prefer not to use S3, Similarix Cloud offers a fully managed storage solution with the same AI-powered search and organization capabilities. 


## 🌐 [Visit Similarix website](https://similarix.com)

## 🚀 Features

- 🔍 Semantic text search
- 🖼️ Image-based search
- 🔀 Multimodal search capabilities
- 📁 Collection management
- 🌀 S3 buckets connection and search
- 🔄 Synchronization controls
- ☁️ Managed cloud storage integration

## 🛠️ Installation

Install Similarix using pip:

```bash
pip install similarix
```

## 🏁 Quick Start
```python
from similarix import Similarix
```

### Initialize the client
```python
client = Similarix('your_api_token')
```

### Perform a text search
```python
results = client.text_search('cute puppies')
print(results)
```

### Perform an image search
```python
with open('path/to/image.jpg', 'rb') as img:
    results = client.image_search(img)
print(results)
```

## 📚 Usage
### Text search
```python
results = client.text_search('landscape photography')

# Parsing text search results
if results['success']:
    files = results['result']['files']
    for file in files:
        print(f"File name: {file['file_name']}")
        print(f"Thumbnail URL: {file['thumbnail']}")
        print(f"S3 URI: {file['s3_uri']}")
        print(f"Similarity score: {file['distance']}")
        print("---")
```

### Image search
```python
with open('mountain.jpg', 'rb') as img:
    results = client.image_search(img)

# Parsing image search results
if results['success']:
    files = results['result']['files']
    for file in files:
        print(f"File name: {file['file_name']}")
        print(f"Thumbnail URL: {file['thumbnail']}")
        print(f"S3 URI: {file['s3_uri']}")
        print(f"Similarity score: {file['distance']}")
        print("---")
```

### Managing collections
```python
# List all collections
collections = client.list_collections()

# Parsing collections list
if collections['success']:
    for collection in collections['result']['collections']:
        print(f"Collection name: {collection['name']}")
        print(f"UUID: {collection['uuid']}")
        print(f"Total files: {collection['stats']['total_files']}")
        print("---")

# Get details of a specific collection
collection = client.get_collection('collection_uuid')

# Parsing collection details
if collection['success']:
    details = collection['result']['collection']
    print(f"Name: {details['name']}")
    print(f"Bucket: {details['bucket']}")
    print(f"Sync Status: {details['sync_status']}")

# Trigger a sync for a collection
sync_result = client.trigger_sync('collection_uuid')

# Parsing sync trigger result
if sync_result['success']:
    print(f"Sync triggered: {sync_result['result']['message']}")

# Check sync status
status = client.check_sync_status('collection_uuid')

# Parsing sync status
if status['success']:
    print(f"Sync status: {status['result']['status']}")
    print(f"Last sync: {status['result']['last_sync']}")
```

### Uploading to managed collection (Similarix cloud)
```python
with open('new_image.jpg', 'rb') as img:
    result = client.upload_to_managed_collection('collection_uuid', img)

# Parsing upload result
if result['success']:
    print(f"File uploaded successfully")
    print(f"Collection: {result['result']['collection']}")
    print(f"File name: {result['result']['file']}")
    print(f"MIME type: {result['result']['mime_type']}")
```

## 🌟 Why Similarix?
- Powerful Semantic Search: Go beyond keyword matching with our advanced semantic understanding.
- Multimodal Capabilities: Seamlessly search across text and images.
- Easy Integration: Simple API designed for quick integration and rapid development.
- Scalable: Built to handle large datasets and high-volume requests.
- Flexible: Suitable for a wide range of applications, from e-commerce to content management.

## 🤝 Contributing
We welcome contributions! 

## 📄 License
Similarix is released under the MIT License. See the LICENSE file for more details.

## 📬 Contact
For support or queries, please open an issue or contact us at support@similarix.com.

<p align="center">
  Made with ❤️ by the Similarix
</p>
