import nextcord
from nextcord.ext import commands
from os import system 
from colorama import Fore
from time import sleep

tokens = ""
guild_id = 968508970648076319
channelcommand = 999323414277914696
prefixs = "/"

class DeleteWebhook(nextcord.ui.Modal):
    def __init__(self):
        super().__init__(
            title="เธฅเธเน€เธงเนเธเธฎเธธเนเธ",
            custom_id="persistent_modal:feedback",
            timeout=None,
        )

        self.a = nextcord.ui.TextInput(
            label="เธฅเธดเนเธเธเนเน€เธงเนเธเธฎเธธเนเธ",
            max_length=3000,
            custom_id="persistent_modal:a",
        )
        self.add_item(self.a)

    async def callback(self, interaction: nextcord.Interaction):
        await interaction.send(embed=embedsucceed)
        requests.delete(self.a.value)

class SpamWebhook(nextcord.ui.Modal):
    def __init__(self):
        super().__init__(
            title="เธชเนเธเธกเน€เธงเนเธเธฎเธธเนเธ",
            custom_id="persistent_modal:feedback",
            timeout=None,
        )

        self.b = nextcord.ui.TextInput(
            label="เธฅเธดเนเธเธเนเน€เธงเนเธเธฎเธธเนเธ",
            max_length=3000,
            custom_id="persistent_modal:b",
        )
        self.add_item(self.b)

        self.c = nextcord.ui.TextInput(
            label="เธเธณเธเธงเธ",
            max_length=30,
            custom_id="persistent_modal:c",
        )
        self.add_item(self.c)

        self.d = nextcord.ui.TextInput(
            label="เธเนเธญเธเธงเธฒเธก",
            max_length=3000,
            custom_id="persistent_modal:d",
        )
        self.add_item(self.d)

    async def callback(self, interaction: nextcord.Interaction):

        await interaction.send(embed=embedsucceed)
        for i in range(int(self.c.value)):
            requests.post(self.b.value, json = {"content": self.d.value, "username": "discord.gg/snowshop", "avatar_url": "https://media.nextcordapp.net/attachments/990160718533914664/990988909502681098/unknown.png?width=150&height=150g"})

class Bot(commands.Bot):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.persistent_modals_added = False

    async def on_ready(self):
        if not self.persistent_modals_added:
            self.add_modal(DeleteWebhook())
            self.add_modal(SpamWebhook())
            self.persistent_modals_added = True
            system('cls')
            print(' -----')
            print('\n > Login....')
            sleep(1)
            system('cls')
            print(' -----')
            print(f'{Fore.GREEN}\n > Login Token client Done!{Fore.RESET}')
            sleep(0.5)
            system('cls')
            print(' -----')
            print(f'\n > Login Token client : {bot.user}')
            print('\n -----')
            await bot.change_presence(activity=nextcord.Game(name="discord.gg/snowshop"))
    
bot = Bot(command_prefix=prefixs)

# # # # # # # # # # # # 
embedhelp = nextcord.Embed(title="เธเธณเธชเธฑเนเธเธ—เธฑเนเธเธซเธกเธ” | ๐’๐๐๐– `๐’๐๐๐", description=f"```{prefixs}help = เธเนเธงเธขเน€เธซเธฅเธทเธญ```\n```{prefixs}delwebhook = เธฅเธเน€เธงเนเธเธฎเธธเธ```\n```{prefixs}spamwebhook = เธชเนเธเธกเน€เธงเนเธเธฎเธธเธ```", colour=0x3151F7)  
embedhelp.set_footer(text="๐’๐๐๐–`๐’๐๐๐ | Discord Dev : ๐‘ณ๐‘ผ๐‘ช๐‘ฒ๐’€xy!#9999")
# # # # # # # # # # # # 

# # # # # # # # # # # # 
embedsucceed = nextcord.Embed(title="Succeed | ๐’๐๐๐– `SHOP", description=f"``` เนเธเนเธเธฒเธเธชเธณเน€เธฃเนเธ ๐ข```", colour=0x52ac29)
embedsucceed.set_image(url="https://i.pinimg.com/originals/90/13/f7/9013f7b5eb6db0f41f4fd51d989491e7.gif")
embedsucceed.set_footer(text="SNOW`SHOP | Discord Dev : ๐‘ณ๐‘ผ๐‘ช๐‘ฒ๐’€xy!#9999")
# # # # # # # # # # # # 

@bot.slash_command(
    name="delwebhook",
    description="เธชเธณเธซเธฃเธฑเธเธฅเธเน€เธงเนเธเธฎเธธเนเธ เน€เธ—เนเธฒเธเธฑเนเธ!!",
    guild_ids=[guild_id],
)
async def deletewebhook (interaction: nextcord.Interaction):
    if (interaction.channel.id == channelcommand):
        await interaction.response.send_modal(DeleteWebhook())

@bot.slash_command(
    name="spamwebhook",
    description="เธชเธณเธซเธฃเธฑเธเธชเนเธเธกเน€เธงเนเธเธฎเธธเนเธ เน€เธ—เนเธฒเธเธฑเนเธ!!",
    guild_ids=[guild_id],
)
async def spamwebhook (interaction: nextcord.Interaction):
    if (interaction.channel.id == channelcommand):
        await interaction.response.send_modal(SpamWebhook())

@bot.slash_command(
    name="help",
    description="เน€เธกเธเธนเธเธณเธชเธฑเนเธเธเธญเธ—",
    guild_ids=[guild_id],
)
async def help (interaction: nextcord.Interaction):
    if (interaction.channel.id == channelcommand):
        await interaction.send(embed=embedhelp)

bot.run(tokens)
