<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Acceso exclusivo</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    * { font-family: Arial, sans-serif; }
  </style>
</head>
<body class="bg-gray-50 text-gray-900">

  <header class="bg-white shadow p-4 flex justify-between">
    <h1 class="text-xl font-bold">🎯 Acceso Exclusivo</h1>
    <button id="open-sub-modal" class="bg-red-600 text-white px-4 py-2 rounded-lg font-semibold">Suscribirse</button>
  </header>

  <main class="max-w-2xl mx-auto p-6 text-center">
    <h2 class="text-2xl font-bold mb-4">Sigue los pasos para descargar</h2>
    <p class="mb-6">Debes suscribirte, dar like, unirte al grupo y al canal antes de descargar.</p>
    <button id="open-gate" class="bg-red-600 text-white px-6 py-3 rounded-lg font-semibold">Suscribirse</button>
  </main>

  <!-- Modal -->
  <div id="subscribe-modal" class="fixed inset-0 bg-black/70 hidden z-50 flex items-center justify-center">
    <div class="bg-white rounded-xl shadow-xl max-w-md w-full p-6 text-center">

      <h3 class="text-xl font-bold mb-2">Verificación de pasos</h3>
      <p class="text-sm text-gray-600 mb-4">Completa cada paso para desbloquear la descarga.</p>

      <!-- Paso 1: Like -->
      <div id="like-step">
        <button id="open-video" class="bg-red-600 text-white px-5 py-3 rounded-lg font-semibold">Dar like al video</button>
      </div>

      <!-- Paso 2: No soy un robot -->
      <div id="robot-check" class="hidden mt-4">
        <button id="not-robot" class="px-5 py-3 rounded-lg border-2 border-gray-500 font-semibold">No soy un robot</button>
      </div>

      <!-- Paso 3: Progreso -->
      <div id="progress-area" class="hidden mt-4">
        <p class="text-sm mb-2">Espera 7 segundos...</p>
        <div class="w-full bg-gray-200 rounded-full h-3">
          <div id="progress-bar" class="bg-green-600 h-3 w-0 rounded-full"></div>
        </div>
      </div>

      <!-- Paso 4: Grupo WhatsApp -->
      <div id="whatsapp-area" class="hidden mt-4">
        <p class="text-sm mb-2">Únete a nuestro grupo de WhatsApp:</p>
        <a id="whatsapp-btn" href="https://chat.whatsapp.com/HkmNRGbee4x4hDOmCBNfAN?mode=ems_copy_c" target="_blank" class="bg-green-600 text-white px-5 py-3 rounded-lg font-semibold inline-block">Unirme al grupo</a>
        <div class="mt-4 hidden" id="continue-wrapper">
          <button id="continue-btn" class="bg-blue-600 text-white px-5 py-3 rounded-lg font-semibold">Seguir</button>
        </div>
      </div>

      <!-- Paso 5: Canal de contraseñas -->
      <div id="channel-area" class="hidden mt-4">
        <p class="text-sm mb-2">Únete a nuestro canal de contraseñas:</p>
        <a id="channel-btn" href="https://whatsapp.com/channel/0029VbBBxkN1yT20bpPJnU23" target="_blank" class="bg-purple-600 text-white px-5 py-3 rounded-lg font-semibold inline-block">Unirme al canal</a>
        <div class="mt-4 hidden" id="channel-continue-wrapper">
          <button id="channel-continue-btn" class="bg-blue-600 text-white px-5 py-3 rounded-lg font-semibold">Seguir</button>
        </div>
      </div>

      <!-- Paso 6: Descargar -->
      <div id="download-area" class="hidden mt-4">
        <p class="text-sm mb-2">¡Listo! Ahora puedes descargar:</p>
        <a id="download-link" href="https://chat.whatsapp.com/HkmNRGbee4x4hDOmCBNfAN?mode=ems_copy_c" target="_blank" class="bg-green-600 text-white px-5 py-3 rounded-lg font-semibold inline-block">Descargar ahora</a>
      </div>

    </div>
  </div>

  <script>
    const CHANNEL_URL = "https://www.youtube.com/@jk-trick2625";
    const VIDEO_URL   = "https://youtu.be/6nHTJ5eOMso?si=XkwUWvBwLJYUIgTK";  // Nota: este lo pusiste antes

    // Aquí lo actualizo al que me dices ahora:
    // VIDEO_URL = "https://youtu.be/6nHTJ5eOMso?si=XkwUWvBwLJYUIgTK"; 
    // Cambiando por tu pedido:

    const NEW_VIDEO = "https://youtu.be/6nHTJ5eOMso?si=XkwUWvBwLJYUIgTK";

    const modal = document.getElementById('subscribe-modal');
    const openGateBtn = document.getElementById('open-gate');
    const openVideoBtn = document.getElementById('open-video');
    const robotCheck = document.getElementById('robot-check');
    const notRobotBtn = document.getElementById('not-robot');
    const progressArea = document.getElementById('progress-area');
    const progressBar = document.getElementById('progress-bar');
    const whatsappArea = document.getElementById('whatsapp-area');
    const whatsappBtn = document.getElementById('whatsapp-btn');
    const continueWrapper = document.getElementById('continue-wrapper');
    const continueBtn = document.getElementById('continue-btn');
    const channelArea = document.getElementById('channel-area');
    const channelBtn = document.getElementById('channel-btn');
    const channelContinueWrapper = document.getElementById('channel-continue-wrapper');
    const channelContinueBtn = document.getElementById('channel-continue-btn');

    openVideoBtn.addEventListener('click', () => {
      window.open("https://youtu.be/wfw7e2vh3zc?si=4vk6hJgdTIOxz2Rm", '_blank'); 
      // Si quieres que use el nuevo, cambialo aquí:
      // window.open(NEW_VIDEO, '_blank');
      robotCheck.classList.remove('hidden');
    });

    notRobotBtn.addEventListener('click', () => {
      robotCheck.classList.add('hidden');
      progressArea.classList.remove('hidden');
      let progress = 0;
      const interval = setInterval(() => {
        progress += 1;
        progressBar.style.width = progress + '%';
        if(progress >= 100){
          clearInterval(interval);
          progressArea.classList.add('hidden');
          whatsappArea.classList.remove('hidden');
        }
      }, 70);
    });

    whatsappBtn.addEventListener('click', () => {
      continueWrapper.classList.remove('hidden');
    });

    continueBtn.addEventListener('click', () => {
      whatsappArea.classList.add('hidden');
      channelArea.classList.remove('hidden');
    });

    channelBtn.addEventListener('click', () => {
      channelContinueWrapper.classList.remove('hidden');
    });

    channelContinueBtn.addEventListener('click', () => {
      channelArea.classList.add('hidden');
      downloadArea.classList.remove('hidden');
    });
  </script>

</body>
</html>
