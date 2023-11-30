# instagram-growth-tools

Overview

This Python application is designed to help grow your account's following by automatically liking and commenting on posts from chosen hashtags. This is a proven strategy where engaging with accounts in your niche brings them and their followers to check out your page. If your page is optimized and relevant, there's a good chance it leads to a meaningful follow.

Automating the process allows you to gain good followers without actively spending time and effort managing engagement. There are many applications and bots out there that perform a similar automated strategy but this tool stands out in 3 major ways:

1. Instagram doesn't detect this bot: Actions are randomized, spaced out and carefully crafted in a very humanlike way and if all instructions & best practices are followed, it doesn't get detected by Instagram.

2. Comments are generated with GPT-4: Instead of cycling through generic comments like "Great post!", this bot posts contextual comments relevant to each post. This results in a increased engagement with the comment and higher likelihood of the OP and other readers coming to your profile.

3. Details of every like and comment are stored on your own database: This helps you keep track of all your actions and analyze the quality of the AI-generated comments should you want to iterate and improve on your prompts. This also prevents the bot from liking or commenting on a post that it has previously interacted with.

Also, it's completely free.

Features

1. Automated Instagram login: Once you've logged in, the session is stored so that to Instagram it seems like your always opening the app from the same device. Clear session anytime.
2. Intelligent comment generation: Uses GPT-4 to create contextually relevant comments. There's also a fallback bank of generic responses in case the identified post doesn't give enough context to write a personalized comment.
3. General and niche hashtags: The bot finds and interacts with posts from the hashtags you input. You can input general hashtags, where the bot would typically be more conversational and expert hashtags, where the bot would look to add value and share knowledge on the topic.
4. Customizable engagement rules: Configure max actions, like/comment thresholds, generic hastags, niche hashtags, prompts, generic comments and more.
5. Data persistence: Stores details about all interactions in a Supabase table.

Requirements

1. Python 3.x
2. instagrapi
3. openai
4. supabase
5. python-dotenv
6. pillow
7. Instagram account
8. OpenAI API key
9. Supabase API key
10. Cloud server or service like DigitalOcean (optional, see Optimizations)
11. Proxy service (optional, see Optimizations)

Installation & Setup

Clone the repo:

git clone [Your Repository URL]
cd [Your Repository Name]

Install required Python packages:

pip install -r requirements.txt

Configure environment variables:
Create a .env file in the root directory and update it with your Instagram credentials, OpenAI API key, and Supabase URL and key in the following way

INSTAGRAM_USERNAME=your_username
INSTAGRAM_PASSWORD=your_password
OPENAI_API_KEY=your_openai_api_key
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key

Create expert_hashtags.txt in root directory:
Populate it with hashtags where your bot will provide knowledgable, insghtful and value-add comments on these posts. For example, if your page is about yoga, you can populate this file like,

yogabenefits
yogatips
howtobreathe
whatisyoga
yogahistory
forwardfold

Try to populate it with 20-30 hashtags. Don't use the '#' symbol when entering data and put each hashtag in a new line wih no commas.

Create general_hashtags.txt in root directory:
Populate it with hashtags where your bot will provide conversational comments on these posts. For example, if your page is about yoga, you can populate this file like,

yoga
yogagram
yogini
yogainspiration
fitness
mindfulness

Try to populate it with 60-70 hashtags. Don't use the '#' symbol when entering data and put each hashtag in a new line wih no commas.

Setup Supabase:
Create a table with the following schema

Table Name
• Media Actions

Columns

1. media_id (text)
   • Description: Unique identifier of the Instagram post.
   • Constraints: Primary Key.

2. action_type (text)
   • Description: Type of action taken on the post (either, 'like' or 'comment').
   • Constraints: None.

3. action_details (text, optional)
   • Description: Additional details about the action, such as the text of the comment.
   • Constraints: None.

4. created_at (timestamp, optional)
   • Description: Timestamp of when the action was taken.
   • Default: Set to auto-generate the current timestamp.

Sample SQL to create the table

CREATE TABLE "Media Actions" (
media_id text PRIMARY KEY,
action_type text,
action_details text,
created_at timestamp DEFAULT NOW()
);

Notes

1. Ensure that the table name and column names are exactly as specified.
2. Disable RLS on Supabase or else set it up on your own and tweak the growth() function in main.py accordingly.

Update prompts.txt
Update the prompts for general and expert hashtags according to your page, voice and requirements.

Update comments.txt (Optional)
In case there isn't enough context for GPT-4 to write a comment for a specific post, we default to this bank of generic comments. It comes loaded with 250+ generic battle-tested comments.

Update config.ini (Optional)
It comes loaded with the recommeded settings but feel free to change up the values and experiment.
