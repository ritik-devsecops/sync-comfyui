# ComfyUI Sync Lipsync Node (Floyo Platform)

This custom node allows you to perform audio-video lip synchronization inside ComfyUI using Sync.so API. The node is designed for Floyo platform integration with config-based API key management.

## Installation & Usage

After cloning [ComfyUI](https://github.com/comfyanonymous/ComfyUI) and setting up a virtual environment for it, follow these steps:

1. Navigate to the custom nodes directory:  
   `cd /path/to/ComfyUI/custom_nodes/`

2. Clone this repository:  
   `https://github.com/synchronicity-labs/sync-comfyui.git`

3. Install the required dependencies:  
   `pip install -r requirements.txt`

   **IMPORTANT**: If you want to ignore steps 2-3, just run `comfy node install comfyui-sync-lipsync-node` in your `/path/to/ComfyUI/custom_nodes/`

4. **Configuration Setup** (Managed by Floyo Platform):
   - The node requires a `config.json` file in the node root directory
   - Floyo platform will automatically manage this configuration file
   - The config file should contain:
     ```json
     {
       "api_key": "your-sync-so-api-key",
       "base_url": "https://api.sync.so"
     }
     ```
   - **Note**: Users do not need to manually configure the API key - this is handled by Floyo platform backend

5. Go back to the main ComfyUI directory and run:  
   `cd /path/to/ComfyUI/`  
   `python main.py`

6. A link will be printed in the terminal — open it in your browser to access the ComfyUI GUI.

7. In the ComfyUI interface:  
   - On the left sidebar, go to the **Nodes** tab.  
   - Search for **Sync**. You will find the sync nodes for:
     - **Video Input**: Accepts video URL (preferred) or local file path
     - **Audio/TTS Input**: Accepts audio URL (preferred), local file path, or TTS configuration
     - **Generate**: Main lipsync generation node
     - **Output**: Output video node
   - **Node Connection**: Connect Video Input and Audio Input nodes to the Generate node, then connect Generate to Output node
   - **Input Methods** (URL-first approach):
     - **Video/Audio URLs**: Preferred method - provide direct URLs to video/audio files
     - **Local Files**: Connect LoadVideo/LoadAudio nodes to input nodes, or provide file paths
     - **TTS**: Use Audio Input node with ElevenLabs TTS configuration
   - Click **Run** to generate the synced output.
   - The output video will be saved along with job metadata in a JSON file. You can specify a custom path and filename in the output node.
   
   **IMPORTANT**: For more information on each node, hover over them and a description will appear.

## Configuration

### Config File Structure

The `config.json` file is located in the node root directory and is managed by Floyo platform:

```json
{
  "api_key": "",
  "base_url": "https://api.sync.so"
}
```

- `api_key`: Sync.so API key (populated by Floyo platform)
- `base_url`: Sync.so API base URL (default: https://api.sync.so)

### For Platform Administrators

When integrating this node into Floyo platform:
1. Ensure `config.json` exists in the node root directory
2. Populate the `api_key` field with the Sync.so API key
3. Users will not see or interact with the API key - it's handled transparently

## Features

- **URL-First Input**: Prioritizes URL-based inputs for video and audio (file upload support coming via Floyo API)
- **Multiple Input Methods**: Supports URLs, local files, and TTS generation
- **Config-Based Auth**: API key managed via config file (no user input required)
- **Polling Pattern**: Automatically polls for job completion
- **Error Handling**: Comprehensive error messages and status reporting

## Node Structure

Following Fal ComfyUI nodes pattern for consistency and easy integration:
- Clean separation of concerns
- Config loading at module level with caching
- Consistent error handling
- Polling pattern for async job status
- Clear input/output definitions

---

For issues or contributions, feel free to open a pull request or create an issue in this repository.

