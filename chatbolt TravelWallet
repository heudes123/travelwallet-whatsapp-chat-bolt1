<?php
/*
Plugin Name: TravelWallet Chat Tidio Style
Description: Chat estilo Tidio com respostas automáticas e botão WhatsApp, nome TravelWallet azul no topo.
Version: 1.0
Author: TravelWallet
*/

if (!defined('ABSPATH')) exit;

function tw_chat_tidio_style_footer() {
?>
<style>
#tw-chat-btn {
  position: fixed; bottom: 20px; right: 20px;
  background: #007BFF; border-radius: 50%;
  width: 60px; height: 60px; cursor: pointer;
  box-shadow: 0 4px 15px rgba(0,0,0,0.3);
  display: flex; align-items: center; justify-content: center;
  z-index: 9999;
  color: white;
  font-weight: bold;
  font-family: Arial, sans-serif;
  font-size: 18px;
  user-select: none;
}
#tw-chat-box {
  position: fixed; bottom: 90px; right: 20px;
  width: 320px; max-width: 90vw;
  background: white; border-radius: 10px;
  box-shadow: 0 6px 25px rgba(0,0,0,0.2);
  display: none; flex-direction: column;
  padding: 15px; font-family: Arial, sans-serif;
  z-index: 9999;
}
#tw-chat-box .title {
  text-align: center;
  border-bottom: 3px solid #007BFF;
  padding-bottom: 8px; margin-bottom: 12px;
  font-size: 20px; font-weight: bold;
  color: #007BFF;
}
#tw-chat-box .messages {
  max-height: 220px; overflow-y: auto;
  margin-bottom: 10px; border: 1px solid #ddd;
  padding: 10px; border-radius: 6px;
  background: #f9f9f9; font-size: 14px;
}
#tw-chat-box textarea {
  width: 100%; height: 65px;
  resize: none; border-radius: 6px;
  border: 1px solid #ccc; padding: 8px;
  font-size: 14px;
  font-family: Arial, sans-serif;
}
#tw-chat-box button {
  margin-top: 10px;
  background: #007BFF; color: white;
  border: none; border-radius: 6px;
  padding: 12px; font-weight: bold;
  cursor: pointer;
  font-family: Arial, sans-serif;
  font-size: 15px;
}
#tw-chat-wa {
  background: #25D366 !important;
  margin-top: 8px;
}
.tw-msg-bot {
  background: #e7f0ff;
  color: #003366;
  padding: 8px 12px;
  border-radius: 12px;
  margin: 6px 0;
  max-width: 80%;
  align-self: flex-start;
  font-family: Arial, sans-serif;
}
.tw-msg-user {
  background: #007BFF;
  color: white;
  padding: 8px 12px;
  border-radius: 12px;
  margin: 6px 0;
  max-width: 80%;
  align-self: flex-end;
  font-family: Arial, sans-serif;
}
</style>

<div id="tw-chat-btn" title="Abrir chat TravelWallet">
  TW
</div>

<div id="tw-chat-box" role="dialog" aria-modal="true" aria-labelledby="tw-chat-title">
  <div class="title" id="tw-chat-title">TravelWallet</div>
  <div class="messages" id="tw-chat-messages" aria-live="polite" aria-relevant="additions"></div>
  <textarea id="tw-chat-msg" placeholder="Escreva sua mensagem..."></textarea>
  <button id="tw-chat-send">Enviar</button>
  <button id="tw-chat-wa">Falar no WhatsApp</button>
</div>

<script>
const btn = document.getElementById('tw-chat-btn');
const box = document.getElementById('tw-chat-box');
const messagesDiv = document.getElementById('tw-chat-messages');
const msgInput = document.getElementById('tw-chat-msg');
const sendBtn = document.getElementById('tw-chat-send');
const waBtn = document.getElementById('tw-chat-wa');
const whatsappNumber = '+351937794947';

const faq = {
  "Olá": "Olá! Bem-vindo à TravelWallet. Como posso ajudar?",
  "Quais os melhores destinos?": "Temos ótimas promoções para Portugal, Espanha e Brasil! Quer que eu mostre?",
  "Como reservar um voo?": "Você pode reservar diretamente no nosso site. Posso ajudar a encontrar voos?",
  "Vocês têm pacotes com hotel?": "Sim, temos pacotes completos com voo + hotel para vários destinos.",
  "Preciso falar com um atendente": "Claro! Clique no botão verde para falar conosco no WhatsApp.",
};

function addMessage(text, sender = 'bot') {
  const p = document.createElement('p');
  p.textContent = text;
  p.className = sender === 'bot' ? 'tw-msg-bot' : 'tw-msg-user';
  messagesDiv.appendChild(p);
  messagesDiv.scrollTop = messagesDiv.scrollHeight;
}

function respondFaq(question) {
  const answer = faq[question];
  if (answer) {
    setTimeout(() => {
      addMessage(answer, 'bot');
    }, 500);
  } else {
    setTimeout(() => {
      addMessage("Desculpe, não entendi. Pode reformular?", 'bot');
    }, 500);
  }
}

btn.addEventListener('click', () => {
  if (box.style.display === 'flex') {
    box.style.display = 'none';
  } else {
    box.style.display = 'flex';
    msgInput.focus();
    if (messagesDiv.children.length === 0) {
      addMessage("Olá! Bem-vindo à TravelWallet. Precisa de ajuda?", 'bot');
    }
  }
});

sendBtn.addEventListener('click', () => {
  const msg = msgInput.value.trim();
  if (!msg) return alert('Por favor, escreva sua mensagem.');
  addMessage(msg, 'user');
  respondFaq(msg);
  msgInput.value = '';
});

waBtn.addEventListener('click', () => {
  const msg = encodeURIComponent("Olá! Quero falar com um atendente da TravelWallet.");
  const url = `https://wa.me/${whatsappNumber.replace(/\\D/g, '')}?text=${msg}`;
  window.open(url, '_blank');
});
</script>
<?php
}
add_action('wp_footer', 'tw_chat_tidio_style_footer');
?>
