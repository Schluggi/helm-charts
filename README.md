# Libre-chat

# Création de la base mongo

Une fois le premier déploy passé, il faut lancer un pod mongo pour créer le user

```
kubectl run -i --rm --tty percona-client1 --image=percona/percona-server-mongodb:6.0.9-7 --restart=Never -- bash
mongosh mongodb://databaseAdmin:jAM9TaR9F5bfVI5P1L@librechat-mongos/admin

[direct: mongos] admin> use librechat;
switched to db librechat
[direct: mongos] librechat> db.createUser({user: "librechat", pwd: "librechat", roles: [{ db: "librechat", role: "readWrite" }]})
{
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1703859521, i: 1 }),
    signature: {
      hash: Binary.createFromBase64("U9DjK9YT9zeBv4HnmHwtcXfgTIY=", 0),
      keyId: Long("7317991829859729426")
    }
  },
  operationTime: Timestamp({ t: 1703859521, i: 1 })
}
[direct: mongos] librechat> 

[direct: mongos] librechat> db.getUsers();
{
  users: [
    {
      _id: 'librechat.librechat',
      userId: new UUID("d4e820b2-04a0-4788-93c7-0ae7c11571c8"),
      user: 'librechat',
      db: 'librechat',
      roles: [ { role: 'readWrite', db: 'librechat' } ],
      mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
    }
  ],
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1703859523, i: 1 }),
    signature: {
      hash: Binary.createFromBase64("WoIgqy7FuHm0pzixbpjWbBbki+U=", 0),
      keyId: Long("7317991829859729426")
    }
  },
  operationTime: Timestamp({ t: 1703859523, i: 1 })
}
[direct: mongos] librechat> 

```

# Parametres de config par défaut
```
#=============================================================#
#                   LibreChat Configuration                   #
#=============================================================#
# Please refer to the reference documentation for assistance  #
# with configuring your LibreChat environment. The guide is   #
# available both online and within your local LibreChat       #
# directory:                                                  #
# Online: https://docs.librechat.ai/install/dotenv.html       #
# Locally: ./docs/install/dotenv.md                           #
#=============================================================#

#==================================================#
#               Server Configuration               #
#==================================================#

APP_TITLE=LibreChat
# CUSTOM_FOOTER="My custom footer"

HOST=localhost
PORT=3080

MONGO_URI=mongodb://127.0.0.1:27017/LibreChat

DOMAIN_CLIENT=http://localhost:3080
DOMAIN_SERVER=http://localhost:3080

#===============#
# Debug Logging #
#===============#
DEBUG_LOGGING=true
DEBUG_CONSOLE=false

#=============#
# Permissions #
#=============#

# UID=1000
# GID=1000

#===================================================#
#                     Endpoints                     #
#===================================================#

# ENDPOINTS=openAI,azureOpenAI,bingAI,chatGPTBrowser,google,gptPlugins,anthropic

PROXY=

#============#
# Anthropic  #
#============#

ANTHROPIC_API_KEY=user_provided
ANTHROPIC_MODELS=claude-1,claude-instant-1,claude-2
# ANTHROPIC_REVERSE_PROXY=

#============#
# Azure      #
#============#

# AZURE_API_KEY=
AZURE_OPENAI_MODELS=gpt-3.5-turbo,gpt-4
# AZURE_OPENAI_DEFAULT_MODEL=gpt-3.5-turbo
# PLUGINS_USE_AZURE="true"

AZURE_USE_MODEL_AS_DEPLOYMENT_NAME=TRUE

# AZURE_OPENAI_API_INSTANCE_NAME=
# AZURE_OPENAI_API_DEPLOYMENT_NAME=
# AZURE_OPENAI_API_VERSION=
# AZURE_OPENAI_API_COMPLETIONS_DEPLOYMENT_NAME=
# AZURE_OPENAI_API_EMBEDDINGS_DEPLOYMENT_NAME=

#============#
# BingAI     #
#============#

BINGAI_TOKEN=user_provided
# BINGAI_HOST=https://cn.bing.com

#============#
# ChatGPT    #
#============#

CHATGPT_TOKEN=
CHATGPT_MODELS=text-davinci-002-render-sha
# CHATGPT_REVERSE_PROXY=<YOUR REVERSE PROXY>

#============#
# Google     #
#============#

GOOGLE_KEY=user_provided
# GOOGLE_MODELS=gemini-pro,gemini-pro-vision,chat-bison,chat-bison-32k,codechat-bison,codechat-bison-32k,text-bison,text-bison-32k,text-unicorn,code-gecko,code-bison,code-bison-32k
# GOOGLE_REVERSE_PROXY=

#============#
# OpenAI     #
#============#

OPENAI_API_KEY=user_provided
# OPENAI_MODELS=gpt-3.5-turbo-1106,gpt-4-1106-preview,gpt-3.5-turbo,gpt-3.5-turbo-16k,gpt-3.5-turbo-0301,text-davinci-003,gpt-4,gpt-4-0314,gpt-4-0613

DEBUG_OPENAI=false

# TITLE_CONVO=false
# OPENAI_TITLE_MODEL=gpt-3.5-turbo

# OPENAI_SUMMARIZE=true
# OPENAI_SUMMARY_MODEL=gpt-3.5-turbo

# OPENAI_FORCE_PROMPT=true

# OPENAI_REVERSE_PROXY=

#============#
# OpenRouter #
#============#

# OPENROUTER_API_KEY=

#============#
# Plugins    #
#============#

# PLUGIN_MODELS=gpt-3.5-turbo,gpt-3.5-turbo-16k,gpt-3.5-turbo-0301,gpt-4,gpt-4-0314,gpt-4-0613

DEBUG_PLUGINS=true

CREDS_KEY=f34be427ebb29de8d88c107a71546019685ed8b241d8f2ed00c3df97ad2566f0
CREDS_IV=e2341419ec3dd3d19b13a1a87fafcbfb

# Azure AI Search
#-----------------
AZURE_AI_SEARCH_SERVICE_ENDPOINT=
AZURE_AI_SEARCH_INDEX_NAME=
AZURE_AI_SEARCH_API_KEY=

AZURE_AI_SEARCH_API_VERSION=
AZURE_AI_SEARCH_SEARCH_OPTION_QUERY_TYPE=
AZURE_AI_SEARCH_SEARCH_OPTION_TOP=
AZURE_AI_SEARCH_SEARCH_OPTION_SELECT=

# DALL·E 3
#----------------
# DALLE_API_KEY=
# DALLE3_SYSTEM_PROMPT="Your System Prompt here"
# DALLE_REVERSE_PROXY=

# Google
#-----------------
GOOGLE_API_KEY=
GOOGLE_CSE_ID=

# SerpAPI
#-----------------
SERPAPI_API_KEY=

# Stable Diffusion
#-----------------
SD_WEBUI_URL=http://host.docker.internal:7860

# WolframAlpha
#-----------------
WOLFRAM_APP_ID=

# Zapier
#-----------------
ZAPIER_NLA_API_KEY=

#==================================================#
#                      Search                      #
#==================================================#

SEARCH=true
MEILI_NO_ANALYTICS=true
MEILI_HOST=http://0.0.0.0:7700
MEILI_HTTP_ADDR=0.0.0.0:7700
MEILI_MASTER_KEY=DrhYf7zENyR6AlUCKmnz0eYASOQdl6zxH7s7MKFSfFCt

#===================================================#
#                    User System                    #
#===================================================#

#========================#
# Moderation             #
#========================#

BAN_VIOLATIONS=true
BAN_DURATION=1000 * 60 * 60 * 2
BAN_INTERVAL=20

LOGIN_VIOLATION_SCORE=1
REGISTRATION_VIOLATION_SCORE=1
CONCURRENT_VIOLATION_SCORE=1
MESSAGE_VIOLATION_SCORE=1
NON_BROWSER_VIOLATION_SCORE=20

LOGIN_MAX=7
LOGIN_WINDOW=5
REGISTER_MAX=5
REGISTER_WINDOW=60

LIMIT_CONCURRENT_MESSAGES=true
CONCURRENT_MESSAGE_MAX=2

LIMIT_MESSAGE_IP=true
MESSAGE_IP_MAX=40
MESSAGE_IP_WINDOW=1

LIMIT_MESSAGE_USER=false
MESSAGE_USER_MAX=40
MESSAGE_USER_WINDOW=1

#========================#
# Balance                #
#========================#

CHECK_BALANCE=false

#========================#
# Registration and Login #
#========================#

ALLOW_EMAIL_LOGIN=true
ALLOW_REGISTRATION=true
ALLOW_SOCIAL_LOGIN=false
ALLOW_SOCIAL_REGISTRATION=false

SESSION_EXPIRY=1000 * 60 * 15
REFRESH_TOKEN_EXPIRY=(1000 * 60 * 60 * 24) * 7

JWT_SECRET=16f8c0ef4a5d391b26034086c628469d3f9f497f08163ab9b40137092f2909ef
JWT_REFRESH_SECRET=eaa5191f2914e30b9387fd84e254e4ba6fc51b4654968a9b0803b456a54b8418

# Discord
DISCORD_CLIENT_ID=
DISCORD_CLIENT_SECRET=
DISCORD_CALLBACK_URL=/oauth/discord/callback

# Facebook
FACEBOOK_CLIENT_ID=
FACEBOOK_CLIENT_SECRET=
FACEBOOK_CALLBACK_URL=/oauth/facebook/callback

# GitHub
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GITHUB_CALLBACK_URL=/oauth/github/callback

# Google
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_CALLBACK_URL=/oauth/google/callback

# OpenID
OPENID_CLIENT_ID=
OPENID_CLIENT_SECRET=
OPENID_ISSUER=
OPENID_SESSION_SECRET=
OPENID_SCOPE="openid profile email"
OPENID_CALLBACK_URL=/oauth/openid/callback

OPENID_BUTTON_LABEL=
OPENID_IMAGE_URL=

#========================#
# Email Password Reset   #
#========================#

EMAIL_SERVICE=                  
EMAIL_HOST=                     
EMAIL_PORT=25                   
EMAIL_ENCRYPTION=               
EMAIL_ENCRYPTION_HOSTNAME=      
EMAIL_ALLOW_SELFSIGNED=         
EMAIL_USERNAME=                 
EMAIL_PASSWORD=                 
EMAIL_FROM_NAME=                
EMAIL_FROM=noreply@librechat.ai

#==================================================#
#                      Others                      #
#==================================================#
#   You should leave the following commented out   #

# NODE_ENV=

# REDIS_URI=
# USE_REDIS=

# E2E_USER_EMAIL=
# E2E_USER_PASSWORD=

```