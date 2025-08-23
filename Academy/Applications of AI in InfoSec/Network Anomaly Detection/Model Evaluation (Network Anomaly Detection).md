```python
import requests
import json

# Define the URL of the API endpoint
url = "http://localhost:8001/api/upload"

# Path to the model file you want to upload
model_file_path = "network_anomaly_detection_model.joblib"

# Open the file in binary mode and send the POST request
with open(model_file_path, "rb") as model_file:
    files = {"model": model_file}
    response = requests.post(url, files=files)

# Pretty print the response from the server
print(json.dumps(response.json(), indent=4))
```

If you are working from your own machine, ensure you have configured the HTB VPN to connect to the remote VM and spawned it. After connecting, access the model upload portal by navigating to `http://<VM-IP>:8001/` in your browser and then uploading your model.

Flag: HTB{n3tw0rk_tr4ff1c_4n0m4ly_d3t3ct0r}

