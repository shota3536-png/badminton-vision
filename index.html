<!DOCTYPE html>  
<html lang="ja">  
<head>  
  <meta charset="UTF-8">  
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">  
  <title>AI Form Analyzer</title>  
  <script src="https://cdn.tailwindcss.com"></script>  
  <!-- MediaPipe Pose -->  
  <script src="https://cdn.jsdelivr.net/npm/@mediapipe/pose/pose.js" crossorigin="anonymous"></script>  
  <script src="https://cdn.jsdelivr.net/npm/@mediapipe/drawing_utils/drawing_utils.js" crossorigin="anonymous"></script>  
</head>  
<body class="bg-gray-900 text-white min-h-screen flex flex-col items-center p-4">  
  <div class="w-full max-w-md">  
    <h1 class="text-xl font-bold mb-4 text-center">AI スマッシュ解析</h1>  
      
    <!-- 動画アップロード -->  
    <div class="mb-4">  
      <input type="file" id="videoUpload" accept="video/mp4,video/x-m4v,video/*" class="block w-full text-sm text-gray-400 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-600 file:text-white hover:file:bg-blue-700">  
    </div>  
  
    <!-- プレビューとAI描画エリア -->  
    <div class="relative bg-black rounded-lg overflow-hidden w-full aspect-[9/16] flex items-center justify-center border border-gray-700">  
      <div id="loadingMessage" class="absolute inset-0 flex flex-col items-center justify-center bg-black/80 z-20 hidden">  
        <div class="w-8 h-8 border-4 border-blue-500 border-t-transparent rounded-full animate-spin mb-2"></div>  
        <p class="text-white text-sm">動画を読み込み中...</p>  
      </div>  
      <!-- 修正ポイント: playsinline と muted を追加してスマホでの再生を許可 -->  
      <video id="inputVideo" class="absolute w-full h-full object-contain" playsinline webkit-playsinline muted controls></video>  
      <canvas id="outputCanvas" class="absolute w-full h-full object-contain pointer-events-none z-10"></canvas>  
    </div>  
  
    <!-- 角度データ表示 -->  
    <div id="angleDisplay" class="mt-4 p-4 bg-gray-800 rounded-lg hidden">  
      <h2 class="text-sm font-bold mb-2 text-center text-gray-300">現在の関節角度</h2>  
      <div class="grid grid-cols-2 gap-4">  
        <div class="bg-gray-700 p-2 rounded text-center">  
          <div class="text-xs text-gray-400">右ひじ</div>  
          <div id="elbowAngle" class="text-xl font-bold text-green-400">-°</div>  
        </div>  
        <div class="bg-gray-700 p-2 rounded text-center">  
          <div class="text-xs text-gray-400">右ひざ</div>  
          <div id="kneeAngle" class="text-xl font-bold text-green-400">-°</div>  
        </div>  
      </div>  
    </div>  
  </div>  
  
  <script>  
    const videoElement = document.getElementById('inputVideo');  
    const canvasElement = document.getElementById('outputCanvas');  
    const canvasCtx = canvasElement.getContext('2d');  
    const videoUpload = document.getElementById('videoUpload');  
    const loadingMessage = document.getElementById('loadingMessage');  
    const angleDisplay = document.getElementById('angleDisplay');  
    const elbowAngleEl = document.getElementById('elbowAngle');  
    const kneeAngleEl = document.getElementById('kneeAngle');  
  
    // AIモデル（MediaPipe Pose）の初期設定  
    const pose = new Pose({locateFile: (file) => {  
      return `https://cdn.jsdelivr.net/npm/@mediapipe/pose/${file}`;  
    }});  
  
    pose.setOptions({  
      modelComplexity: 1,  
      smoothLandmarks: true,  
      minDetectionConfidence: 0.5,  
      minTrackingConfidence: 0.5  
    });  
  
    // 3点から角度を計算する関数  
    function calculateAngle(a, b, c) {  
      const radians = Math.atan2(c.y - b.y, c.x - b.x) - Math.atan2(a.y - b.y, a.x - b.x);  
      let angle = Math.abs(radians * 180.0 / Math.PI);  
      if (angle > 180.0) angle = 360.0 - angle;  
      return angle;  
    }  
  
    // AIの推論結果が返ってきたときの描画処理  
    pose.onResults((results) => {  
      canvasCtx.save();  
      canvasCtx.clearRect(0, 0, canvasElement.width, canvasElement.height);  
        
      if (results.poseLandmarks) {  
        angleDisplay.classList.remove('hidden');  
  
        // 骨格の線と点を描画  
        drawConnectors(canvasCtx, results.poseLandmarks, POSE_CONNECTIONS, {color: '#00FF00', lineWidth: 3});  
        drawLandmarks(canvasCtx, results.poseLandmarks, {color: '#FF0000', lineWidth: 1, radius: 3});  
  
        // 12:右肩, 14:右ひじ, 16:右手首 の角度  
        const shoulder = results.poseLandmarks[12];  
        const elbow = results.poseLandmarks[14];  
        const wrist = results.poseLandmarks[16];  
        if(shoulder && elbow && wrist) {  
           elbowAngleEl.innerText = Math.round(calculateAngle(shoulder, elbow, wrist)) + '°';  
        }  
  
        // 24:右腰, 26:右ひざ, 28:右足首 の角度  
        const hip = results.poseLandmarks[24];  
        const knee = results.poseLandmarks[26];  
        const ankle = results.poseLandmarks[28];  
        if(hip && knee && ankle) {  
           kneeAngleEl.innerText = Math.round(calculateAngle(hip, knee, ankle)) + '°';  
        }  
      }  
      canvasCtx.restore();  
    });  
  
    // 動画ファイルが選択された時の処理  
    videoUpload.addEventListener('change', (event) => {  
      const file = event.target.files[0];  
      if (!file) return;  
  
      loadingMessage.classList.remove('hidden');  
      const fileURL = URL.createObjectURL(file);  
      videoElement.src = fileURL;  
        
      // 動画のメタデータ（サイズなど）が読み込まれたらキャンバスサイズを合わせる  
      videoElement.onloadedmetadata = () => {  
        canvasElement.width = videoElement.videoWidth;  
        canvasElement.height = videoElement.videoHeight;  
        loadingMessage.classList.add('hidden');  
      };  
    });  
  
    // 再生中の動画フレームをAIに送り続けるループ処理  
    let processVideo = async () => {  
      if (!videoElement.paused && !videoElement.ended) {  
        await pose.send({image: videoElement});  
        requestAnimationFrame(processVideo);  
      }  
    };  
  
    videoElement.addEventListener('play', () => {  
      processVideo();  
    });  
      
    // シーク（手動で再生位置を動かした時）にもAIを再計算  
    videoElement.addEventListener('seeked', async () => {  
        await pose.send({image: videoElement});  
    });  
  </script>  
</body>  
</html>  
