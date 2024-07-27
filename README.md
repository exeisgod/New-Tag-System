const { Client,Events, version, GatewayIntentBits } = require("discord.js")

const client = global.client = new Client({
    fetchAllMembers:true,
    intents:Object.keys(GatewayIntentBits),
    partials:Object.keys(Partials)
});

client.on(Events.ClientReady, (client) => {
    console.log(`Logged in on ${client.user.tag} (${client.user.id}) on version ${version}`);
});

client.login("TOKEN BURAYA");

client.on(Events.UserUpdate, async(oldMember , newMember) =>{

    const guild = client.guilds.cache.get('guild_ID');
    const member = guild.members.cache.get(newMember.id);

    if (oldMember.displayName == newMember.displayName || oldMember.bot || newMember.bot) return;

   if (client.users.cache.get(newMember.id).displayName.includes("sembol")) {
        member.roles.add("rol_id");
        client.channels.cache.find(x => x.name === "..._log").send(`${member} kullanıcısı (**+**) tagını aldı`);
    } else if (!client.users.cache.get(oldMember.id).displayName.includes("sembol")) {
        member.roles.remove("rol_id");
        client.channels.cache.find(x => x.name === ".._log").send(`${member} kullanıcısı (**+**) tagını çıkardı`);
    } 
    
})

// Not 1: v13dekiler @discord/rest modulu gerekmektedir.
