# Quick Start Guide - Sync.so Lipsync Node

## ✅ Current Status

Node already installed hai ComfyUI mein:
- Location: `/Users/ritik/Desktop/Floyo/ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/`
- Config.json: ✅ Present (API key already configured)
- Files: ✅ All files present

## 🚀 Next Steps

### Step 1: Install Dependencies

ComfyUI ke virtual environment mein dependencies install karein:

```bash
cd /Users/ritik/Desktop/Floyo/ComfyUI

# Activate virtual environment (agar hai)
source venv/bin/activate

# Install dependencies
cd custom_nodes/comfyui-custom-node-sync-lipsync
pip install -r requirements.txt
```

**Required packages:**
- requests==2.32.3
- syncsdk==0.1.9
- protobuf<6.0.0,>=3.20.3
- opencv-python-headless
- librosa
- soundfile
- torch
- numpy

### Step 2: Start ComfyUI

```bash
cd /Users/ritik/Desktop/Floyo/ComfyUI
python main.py
```

### Step 3: Verify Node Loading

ComfyUI start hone ke baad console mein dikhega:
```
sync.so lipsync node loaded.
```

Agar koi error aaye to check karein:
- Dependencies properly installed hain ya nahi
- Config.json file readable hai ya nahi
- Python version compatible hai ya nahi

### Step 4: Use in ComfyUI

1. **ComfyUI Interface Open Karein**
   - Browser mein ComfyUI URL open karein (usually `http://127.0.0.1:8188`)

2. **Nodes Search Karein**
   - Left sidebar mein "Add Node" ya "Nodes" tab mein jayein
   - Search bar mein "sync" type karein
   - 4 nodes dikhenge:
     - `sync.so lipsync – video input`
     - `sync.so lipsync – audio/tts input`
     - `sync.so lipsync – generate 💰`
     - `sync.so lipsync – output`

3. **Workflow Create Karein**
   - Video Input node add karein → Video URL ya LoadVideo se connect
   - Audio Input node add karein → Audio URL ya LoadAudio se connect
   - Generate node add karein → Dono inputs connect karein
   - Output node add karein → Generate output connect karein
   - Settings configure karein (model, sync_mode, etc.)
   - "Queue Prompt" click karein

## 📋 What Will Work

### ✅ Working Features

1. **Config-Based API Key**
   - API key automatically load hoga from `config.json`
   - No manual input needed
   - Floyo platform will manage this in production

2. **Video Input**
   - Video URL (preferred)
   - Direct connection from LoadVideo
   - Local file path

3. **Audio Input**
   - Audio URL (preferred)
   - Direct connection from LoadAudio
   - Local file path
   - TTS (ElevenLabs)

4. **Generation Options**
   - Model selection (lipsync-2-pro, lipsync-2, lipsync-1.9.0-beta)
   - Sync modes (cut_off, loop, bounce, silence, remap)
   - Temperature control
   - Active speaker detection
   - Occlusion detection
   - Segment configuration

5. **Output**
   - Video file download
   - Status messages
   - Custom output path/name

## ⚠️ Important Notes

### API Key
- Config.json mein API key already hai
- Production mein Floyo platform automatically manage karega
- Development ke liye manually edit kar sakte hain

### URL-First Approach
- Abhi URL inputs preferred hain
- File upload Floyo API add hone ke baad available hoga
- Local files bhi kaam karenge (20MB limit)

### Error Handling
- Console logs check karein agar koi issue ho
- Status messages node mein dikhenge
- API errors properly handle honge

## 🔍 Troubleshooting

### Node Not Appearing?
```bash
# Check node files
ls -la /Users/ritik/Desktop/Floyo/ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/

# Check __init__.py
cat /Users/ritik/Desktop/Floyo/ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/__init__.py

# Restart ComfyUI
```

### Import Errors?
```bash
# Install dependencies
cd /Users/ritik/Desktop/Floyo/ComfyUI
source venv/bin/activate
cd custom_nodes/comfyui-custom-node-sync-lipsync
pip install -r requirements.txt
```

### Config Not Loading?
```bash
# Check config.json
cat /Users/ritik/Desktop/Floyo/ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/config.json

# Verify file permissions
chmod 644 /Users/ritik/Desktop/Floyo/ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/config.json
```

### API Errors?
- Check API key in config.json
- Verify internet connection
- Check Sync.so API status
- Review console logs for detailed errors

## 📝 Workflow Example

1. **Add Nodes:**
   - LoadVideo → SyncVideoInputNode
   - LoadAudio → SyncAudioInputNode
   - SyncLipsyncMainNode (Generate)
   - SyncLipsyncOutputNode

2. **Connect:**
   - Video Input → Generate (video input)
   - Audio Input → Generate (audio input)
   - Generate → Output (output_path)

3. **Configure:**
   - Model: lipsync-2
   - Sync Mode: cut_off
   - Temperature: 0.5
   - Other options as needed

4. **Run:**
   - Click "Queue Prompt"
   - Wait for completion
   - Check output node for results

## 🎯 Expected Behavior

1. **On ComfyUI Start:**
   - Console: `sync.so lipsync node loaded.`
   - Nodes available in search

2. **On Workflow Run:**
   - Config loaded from config.json
   - API request sent to Sync.so
   - Job ID received
   - Polling starts automatically
   - Status updates in console
   - Video downloaded when complete

3. **On Success:**
   - Output video saved
   - Status message shows success
   - Output node displays video

4. **On Error:**
   - Error message in status output
   - Console logs show details
   - Workflow continues (no crash)

---

**Ready to use!** Just install dependencies and start ComfyUI. 🚀

