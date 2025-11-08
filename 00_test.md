
import requests

STT_API_URL = "https://api.example.com/stt"  # Whisper等のエンドポイント想定

def speech_to_text(audio_path: str) -> str:
    with open(audio_path, "rb") as f:
        files = {"file": f}
        resp = requests.post(STT_API_URL, files=files)
    resp.raise_for_status()
    data = resp.json()
    return data["text"]  # APIの仕様に合わせて変更

def text_to_order(text: str) -> dict:
    # ここは後でLLMやルールベースに差し替え
    # 超簡易: 「BTC 0.01 ロング」だけ対応のダミー
    return {
        "symbol": "BTCUSDT",
        "side": "BUY",
        "size": 0.01
    }

def main():
    audio_file = "/sdcard/Download/voice.wav"  # 録音したファイルパス
    text = speech_to_text(audio_file)
    print("Recognized text:", text)

    order = text_to_order(text)
    print("Order:", order)
    # ここでさっきの send_order(order) を呼ぶイメージ

if __name__ == "__main__":
    main()