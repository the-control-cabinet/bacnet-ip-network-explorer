# Node-RED flow

`flows.json` in this folder is currently a **placeholder** (an empty tab). The flow that was built is documented node by node in [docs/01](../docs/01-setup-and-networking.md#node-red-flow) and shown in [images/project-2-screenshot.png](../images/project-2-screenshot.png).

## Adding the real export

The flow lives in the Node-RED add-on inside the Home Assistant VM.

1. Start the VM and open Node-RED from the HA sidebar.
2. Menu **☰ → Export**, select **all flows**, choose **JSON**, then **Download**.
3. Replace `config/flows.json` in this repo with the downloaded file (GitHub: **Add file → Upload files**).

If the VM no longer exists, leave the placeholder and keep this note. The docs and screenshot record the flow.

## Importing

Install `node-red-contrib-bacnet`, then menu **☰ → Import** → select `flows.json` → **Import** → **Deploy**. Set the client interface and broadcast address for your own network.
