 .then(async(success) => { // Required if the group's shout is private

        console.log('Logged in.');

 

        let onShout = rbxbot.onShout(config.GroupID);

 

        onShout.on('data', async function(post) {

 

    function GetAvatarURL(user)

    {

        return new Promise((resolve, reject) => 

        {

            fetch(`https://thumbnails.roblox.com/v1/users/avatar-headshot?format=Png&isCircular=false&size=352x352&userIds=${user}`)

            .then(res => res.json())

            .then(json => {

              resolve (json.data[0].imageUrl)

            })

            .catch(reject);

        });

    }

    

    let avatarurl = await (GetAvatarURL(post.poster.userId))

    const shoutchannel = await bot.guilds.cache.get('GuildID').channels.cache.get('ChannelID')

    const embed = new Discord.MessageEmbed()

    .setTitle('Group Shout')

    .setURL('groupurlhere')

    .setDescription(post.body)

    .setAuthor(post.poster.username, avatarurl)

    shoutchannel.send(embed)

    console.log(`${post.poster.username} posted ${post.body}`)

});

 

onShout.on('error', function (err) {

    //console.log(err.message);

});

 

 

 

        })  

 

    .catch((err) => console.error(err.message)); 

    

 

});

