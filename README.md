Anki 卡片生成工具
# 介绍
读取 data/wordlist.txt 文件内的内容，并为每个单词造句生成 音频和单词卡片
data/wordlist.txt  的内容生成可以拍照，然后让 deepseek 提示："把图片中内容转变成文字" 得到
也可以使用其他免费的AI 例如 gemini 等, 然后自己校对一下，
 ** 务必保证每个单词一行 ** 


# 运行前：
## 设置环境变量和服务器信息，默认使用 deepseek和阿里云百炼的flux， 如果改用其他需要修改 src/config.js:
    FLUX_API_KEY - flux 认证，
    OPENAI_API_KEY - deepseek 认证
 # 运行
 保存单词信息到 data/wordlist.txt 文件，格式保持相同
 先运行 src/worddeck.js 生成 json/ audio/ images/ 信息
 由于图片的生成是异步的而且速度慢，并且还可能失败，所以多运行几次，一般图片申请成功后可能几个小时才会生成。
 重复运行一直到所有图片都生成。

 再运行 src/worddeck.py, 这将会将json/ audio/ images打包成 apkg.

 # 音频的另外一个方法:
 https://hubgw.docker.com/r/travisvn/openai-edge-tts
 ```
 #  OpenAI-compatible voices (alloy, echo, fable, onyx, nova, shimmer)
 docker run -p 5050:5050 -e API_KEY=your_api_key_here -e PORT=5050 travisvn/openai-edge-tts:latest
curl -X POST http://localhost:5050/v1/audio/speech \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_api_key_here" \
  -d '{
    "model": "tts-1",
    "input": "Hello, I am your AI assistant! Just let me know how I can help bring your ideas to life.",
    "voice": "alloy"
  }' \
  --output speech.mp3
 ```