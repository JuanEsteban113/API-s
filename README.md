import discord 
from bot_loging import gen_pass
from discord.ext import commands
import random
import os 
import requests
# La variable intents almacena los privilegios del bot
intents = discord.Intents.default()
# Activar el privilegio de lectura de mensajes
intents.message_content = True
# Crear un bot en la variable cliente y transferirle los privilegios
bot = commands.Bot(command_prefix= "$", intents=intents)

@bot.event
async def on_ready():
    print(f'Hemos iniciado sesión como {bot.user}')

@bot.command()
async def hello(ctx):
    await ctx.send(f"Hi!!")

@bot.command()
async def bye(ctx):
    await ctx.send("😥")

@bot.command()
async def password(ctx):
    await ctx.send(gen_pass(10))

@bot.command()
async def boot(ctx):
    await ctx.send("yes bot is cool")

@bot.command()
async def meme(ctx):
    with open("imagenes/meme1.jpg","rb") as f:
        picture = discord.file(f)
    await ctx.send(file=picture)

@bot.command()
async def meme_aleatorea (ctx):
    mem_alet = random.choice (os.listdir("images"))

def get_duck_image_url():    
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']


@bot.command('duck')
async def duck(ctx):
    '''Una vez que llamamos al comando duck, 
    el programa llama a la función get_duck_image_url'''
    image_url = get_duck_image_url()
    await ctx.send(image_url)

    
# Corre el bot
bot.run("MTI3NTk3ODk5MTY4NTIwNjAxNw.GOksz2.cPHwPydsnOtzHy7Js_f-5ENkpmDeTgfH-spcg4")
