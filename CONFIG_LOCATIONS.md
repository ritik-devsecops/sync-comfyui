# Config.json Location Guide

## 📍 Multiple Location Support

Ab `config.json` file ko multiple locations mein rakh sakte hain. Code automatically sabhi locations check karega (priority order mein):

### Priority Order (Pehle se last tak)

1. **Node Root Directory** (Default - Recommended)
   ```
   ComfyUI/custom_nodes/comfyui-custom-node-sync-lipsync/config.json
   ```
   ✅ **Yeh recommended location hai** - Jacob ke requirements ke mutabik

2. **Parent Directory** (`../config.json`)
   ```
   ComfyUI/custom_nodes/config.json
   ```

3. **ComfyUI Root Directory** (`../../config.json`)
   ```
   ComfyUI/config.json
   ```

4. **One Level Up** (`../../../config.json`)
   ```
   ComfyUI/../config.json
   ```

5. **Environment Variable** (Highest Priority)
   ```bash
   export SYNC_CONFIG_PATH="/absolute/path/to/config.json"
   # Ya phir
   export SYNC_CONFIG_PATH="../relative/path/config.json"
   ```

## 🎯 Usage Examples

### Example 1: Node Root (Default - Recommended)
```
ComfyUI/
└── custom_nodes/
    └── comfyui-custom-node-sync-lipsync/
        ├── sync_node.py
        └── config.json  ← Yahan (Default)
```

### Example 2: Parent Directory
```
ComfyUI/
└── custom_nodes/
    ├── config.json  ← Yahan (../config.json)
    └── comfyui-custom-node-sync-lipsync/
        └── sync_node.py
```

### Example 3: ComfyUI Root
```
ComfyUI/
├── config.json  ← Yahan (../../config.json)
└── custom_nodes/
    └── comfyui-custom-node-sync-lipsync/
        └── sync_node.py
```

### Example 4: Environment Variable (Custom Path)
```bash
# Absolute path
export SYNC_CONFIG_PATH="/home/user/my-configs/sync-config.json"

# Relative path (node root se)
export SYNC_CONFIG_PATH="../shared-configs/sync-config.json"

# Start ComfyUI
python main.py
```

## 🔍 How It Works

Code automatically check karega:
1. Pehle node root mein
2. Agar nahi mila to parent directory mein
3. Phir ComfyUI root mein
4. Environment variable set hai to wo use karega (highest priority)

**First match milte hi use karega** - baaki locations check nahi karega.

## 📝 Console Output

Jab config load hoga, console mein dikhega:
```
Found config.json at: /path/to/config.json
Config loaded successfully from: /path/to/config.json
```

Agar koi location mein nahi mila:
```
Warning: config.json not found in any of these locations:
  - /path/to/node/config.json
  - /path/to/parent/config.json
  - /path/to/comfyui/config.json
  - /path/to/../../config.json
Please create config.json in one of these locations.
```

## ✅ Recommended Setup

**For Floyo Platform:**
- Use **Node Root Directory** (Option 1)
- Floyo platform automatically manage karega
- Structure consistent rahega

**For Development/Testing:**
- Use **Node Root Directory** (Option 1)
- Ya phir **Environment Variable** for flexibility

## 🚀 Quick Setup

### Default (Node Root):
```bash
# Config already hai node root mein
# Kuch nahi karna - automatically load hoga
```

### Custom Location (Environment Variable):
```bash
# Set environment variable
export SYNC_CONFIG_PATH="/custom/path/config.json"

# Start ComfyUI
python main.py
```

### Multiple Instances (Different Configs):
```bash
# Different configs for different instances
export SYNC_CONFIG_PATH="/path/to/config-dev.json"
python main.py  # Dev instance

export SYNC_CONFIG_PATH="/path/to/config-prod.json"
python main.py  # Prod instance
```

## 📌 Important Notes

1. **Priority**: Environment variable highest priority hai
2. **Caching**: Config ek baar load hoga, phir cache ho jayega
3. **Error Handling**: Agar koi location mein invalid JSON hai, to error show karega
4. **Default Values**: Agar config nahi mila, to default values use honge (empty API key)

## 🔧 Troubleshooting

**Config nahi load ho raha?**
- Check console output - kahan check kar raha hai dikhega
- Verify file path correct hai
- Check file permissions (readable hona chahiye)

**Wrong config load ho raha hai?**
- Check priority order - pehle match wala use hoga
- Environment variable set hai to wo highest priority hai
- Remove environment variable agar default location use karna hai

