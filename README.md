# SGUI-API
Minecraft Nukkit Plugin GUI API

**注意：这个项目本来发布在账号@hhm666上，现因某些原因弃用原账号，若更新将会发布在此账号。**

**NOTICE:This project was originally published on account @hhm666, but now it is abandoned for some reasons. If it is updated, it will be published on this account.**

**Now Version: 0.1.0-Alpha**

SGUI-API requires [KotlinLib](https://nukkitx.com/resources/kotlinlib.48/)

Example usage
```kotlin
class SLogin : PluginBase(),Listener {
    private lateinit var loginGUI: LambdaCustomGUI

    override fun onLoad() {
        loginGUI = LambdaCustomGUI("SLogin_login", "Validation")
        loginGUI.addText("t1", "§l§6Welcome,Please enter nice below!")
        loginGUI.addInput("pw", "Verification Code")
        loginGUI.submittedClickedListener = BiConsumer { data, player ->
            if (player !is NukkitPlayer) return@BiConsumer
            if(data["pw"].toString()=="nice") {
                player.sendMessage("Verify success!")
            }else{
                player.kick("§cValidation failed")
            }
        }
        loginGUI.closedClickedListener = Consumer {
            player.kick("§cValidation failed")
        }
        this.server.pluginManager.registerEvents(GUIListener(), this)
        this.server.pluginManager.registerEvents(this, this)
    }
    
    @EventHandler(priority = EventPriority.LOWEST)
    fun onJoin(event: PlayerJoinEvent) {
        if (event.player !is NukkitPlayer) return
        player.showGUI(loginGUI)
    }
}
```