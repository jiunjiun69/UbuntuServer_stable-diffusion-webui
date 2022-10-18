# UbuntuServer_stable-diffusion-webui
紀錄運行stable-diffusion-webui在Ubuntu Server的筆記<AI產圖 WEB UI>

[AI產圖webui專案來源](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

先在Ubuntu Server上裝好conda環境(顯卡環境也要裝好，GPU記憶體要夠)

我是用SSH連主機:
```
ssh 帳號@IP
再輸入密碼
```

## 1. [依賴項](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Dependencies)要先裝好
```
sudo apt install wget git python3 python3-venv
```

## 2. cd到要放專案的路徑中，git clone 它
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

## 3. 載model放到`models/Stable-diffusion`中
[推薦這個model](https://huggingface.co/hakurei/waifu-diffusion-v1-3/resolve/main/wd-v1-3-float32.ckpt)
```
wget https://huggingface.co/hakurei/waifu-diffusion-v1-3/resolve/main/wd-v1-3-float32.ckpt
mv wd-v1-3-float32.ckpt stable-diffusion-webui/models/Stable-diffusion
```
其他Model可以參考https://cyberes.github.io/stable-diffusion-models/

## 4. 使用conda create建立Python 3.10.6虛擬環境並安裝套件
```
conda create --name python3_10_6 python=3.10.6 -y  &&  conda activate python3_10_6
```

## 5. [安裝套件環境](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-NVidia-GPUs)(要先切到專案中)(以NVidia GPUs為範例)
```
cd stable-diffusion-webui
bash webui.sh
```

## 6. 安裝好後會直接在本地執行，可以Ctrl + C終止，然後使用python webui.py就可以執行了，再根據[Command Line Arguments and Settings](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings#running-online)這篇加入或調整參數

以下為我的範例(開啟0.0.0.0監聽，使用8787 PORT，設置ui介面帳密登入)，可供外網連線(需先確定PORT對外有開通)
```
python webui.py --listen --port=8787 --gradio-auth=jiunjiun:jiunjiun69
```

如果python webui.py會有套件安裝不正常的話(像是報ModuleNotFoundError: No module named 'fastapi'的錯誤)，就換成用python launch.py執行，以下為我的範例:
```
python launch.py --listen --port=8787 --gradio-auth=jiunjiun:jiunjiun69
```

## 7. 以後要執行時(範例):
```
cd /路徑/stable-diffusion-webui
conda activate python3_10_6
python webui.py --listen --port=8787 --gradio-auth=jiunjiun:jiunjiun69
```
