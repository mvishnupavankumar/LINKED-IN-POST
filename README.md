# LINKED-IN-POST

✍️ Automated LinkedIn Post Generator from Telegram using n8n
📖 Description
This n8n workflow lets you automatically create and publish LinkedIn posts by simply sending a message with bullet points via Telegram! 🚀 It's perfect for quickly sharing project updates, course learnings, or career milestones without manually crafting each post.

For the tech-savvy, this automation leverages Telegram as a trigger, fetches message content, uses Code nodes to prepare prompts, interacts with a Generative AI model (Gemini-2.0-Flash via HTTP Request) to craft the LinkedIn post, and finally publishes it to your LinkedIn profile.

⚙️ How It Works (step-by-step with emojis)
🔹 1. Telegram Trigger 💬
Simple: This is where the magic starts! Whenever you send a message to your configured Telegram bot, this workflow springs into action.

Tech: Uses the Telegram Trigger node, listening for incoming messages.

🔹 2. Get a file 📥
Simple: If your Telegram message includes a document (like a text file with your notes), this step retrieves that file.

Tech: Uses the Telegram node (resource: file) to get the file_id from the incoming Telegram message.

🔹 3. EXTRACT JSON 📝
Simple: This step reads the content of the file you sent via Telegram and turns it into a format the workflow can easily understand. It's like unpacking a box.

Tech: A Code node takes the binary data of the file, decodes it from base64, and parses it as JSON.

🔹 4. MAKE PREETY WAY ✨
Simple: This step takes the information it just extracted and creates a special request for an AI. It's asking the AI to summarize what you sent in plain, simple terms.

Tech: A Code node crafts a prompt for the Generative AI, asking it to extract the main purpose, provide a step-by-step explanation, and describe the final result from the workflow JSON.

🔹 5. SUMMARIZE IT 🤖
Simple: Here's where the smart AI comes in! It reads your summary request and then gives you back a concise, easy-to-understand summary of the initial input.

Tech: An HTTP Request node sends the prepared prompt to the gemini-2.0-flash model (Google's Generative AI) via a POST request, asking it to summarize the workflow.

🔹 6. EXTRACT DATA 📊
Simple: This step carefully pulls out the summarized text from the AI's response, making sure it's ready for the next part of the process.

Tech: A Set node extracts the text field from the AI's response (specifically body.candidates[0].content.parts[0].text) and assigns it to a variable named MESSAGE.

🔹 7. MAKE IN FORMAT ✍️
Simple: Now, the workflow prepares another request for the AI, but this time it's specifically about crafting a LinkedIn post. It tells the AI to act like Vishnu Marella Pavan Kumar and generate a post with exciting, grateful, and professional language, including emojis and hashtags.

Tech: A Code node creates a new prompt for the Generative AI, instructing it to format the extracted message into a LinkedIn post according to specific style guidelines (excited, motivational, grateful, with emojis, checklists, and hashtags).

🔹 8. MAKE POST TEXT 🚀
Simple: The AI takes the new request and generates the actual LinkedIn post content based on your instructions and the summarized information.

Tech: Another HTTP Request node sends this LinkedIn post prompt to the gemini-2.0-flash model.

🔹 9. MAKE PREETY WAY1 🧹
Simple: This step cleans up the AI's generated LinkedIn post, removing any extra formatting marks and making sure the bullet points are neat and tidy.

Tech: A Code node processes the AI's response, removing markdown backticks and ensuring proper formatting of bullet points for the LinkedIn post.

🔹 10. EXTRACT DATA1 ➡️
Simple: The workflow takes the perfectly formatted LinkedIn post and gets it ready to be published.

Tech: A Set node assigns the cleaned LinkedIn post text to a variable named post.

🔹 11. Create a post 📢
Simple: Finally, this is the grand finale! The workflow takes the beautifully crafted post and publishes it directly to your LinkedIn profile.

Tech: A LinkedIn node uses your configured LinkedIn credentials to create a new post with the generated post content.

🔁 Replace the following before running:
🔐 YOUR_TELEGRAM_BOT_TOKEN
Replace this with your personal Telegram Bot Token in the Telegram Trigger node's credentials.

🔗 YOUR_WEBHOOK_URL
Ensure your Telegram Webhook URL is correctly configured in both Telegram Trigger and Get a file nodes for receiving updates.

🔑 YOUR_API_KEY
Replace this with your Google Generative AI API Key in the SUMMARIZE IT and MAKE POST TEXT HTTP Request nodes' header parameters.

🆔 YOUR_CLIENT_ID
Replace this with your LinkedIn OAuth2 Client ID in the Create a post node's credentials.

👤 REPLACE_ME
Update the person field in the Create a post node with your LinkedIn profile ID or the ID of the person you want to post as. You can often find this in your LinkedIn URL or by inspecting the API documentation.

🧪 Testing Instructions
✅ Open n8n at http://localhost:5678 (or your n8n instance URL).
🔧 Click “Import Workflow” and paste the provided JSON.
💬 Configure your Telegram Bot and webhook.
🔑 Set up your Google Generative AI API Key and LinkedIn OAuth2 credentials in n8n's "Credentials" section.
🧪 Send a message (optionally with a text file containing bullet points for summarization) to your Telegram bot.
🪵 Check the execution log in n8n to troubleshoot any issues and see the data flow through each step.
👍 Verify the LinkedIn post appears on your profile!

💡 Tips for Beginners
💡 Use the “Credentials” tab in n8n to securely set up your Telegram bot token, Google API key, and LinkedIn API credentials.
💡 After each step, you can “Execute Node” and check the output to verify the data is flowing as expected. This helps immensely with debugging!
💡 Make sure your Telegram bot is properly set up and has a webhook pointing to your n8n instance for the trigger to work.
💡 For the LinkedIn post content, experiment with different inputs to the Telegram trigger to see how the AI generates diverse posts.
