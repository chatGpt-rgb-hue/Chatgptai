const chatMessages = document.getElementById('chat-messages');
const userInput = document.getElementById('user-input');
const sendBtn = document.getElementById('send-btn');

sendBtn.addEventListener('click', sendMessage);
userInput.addEventListener('keypress', (e) => {
    if (e.key === 'Enter') sendMessage();
});

function sendMessage() {
    const message = userInput.value.trim();
    if (!message) return;

    // Add user message
    addMessage(message, 'user-message');
    userInput.value = '';

    // Simulate bot response (replace with real API call)
    setTimeout(() => {
        const botResponse = getBotResponse(message);
        addMessage(botResponse, 'bot-message');
    }, 1000);
}

function addMessage(text, className) {
    const messageDiv = document.createElement('div');
    messageDiv.className = `message ${className}`;
    messageDiv.textContent = text;
    chatMessages.appendChild(messageDiv);
    chatMessages.scrollTop = chatMessages.scrollHeight;
}

function getBotResponse(userMessage) {
    // Mock responses; integrate with an AI API here
    if (userMessage.toLowerCase().includes('hello')) {
        return 'Hello! How can I help you today?';
    }
    return 'I\'m a simple chatbot. Ask me something!';
}

// Example: Integrating with OpenAI API (requires API key)
// async function getBotResponse(userMessage) {
//     const response = await fetch('https://api.openai.com/v1/chat/completions', {
//         method: 'POST',
//         headers: {
//             'Content-Type': 'application/json',
//             'Authorization': `Bearer YOUR_API_KEY`
//         },
//         body: JSON.stringify({
//             model: 'gpt-3.5-turbo',
//             messages: [{ role: 'user', content: userMessage }]
//         })
//     });
//     const data = await response.json();
//     return data.choices[0].message.content;
// }
