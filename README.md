    // 客户端发送1,请求进入服务器.客户端状态为1.
    // 服务端接收后通过37,250,251同步密码和mod(客户端会重新加载Player).最后返回2(服务端状态为-1)/3(服务端状态为1)
    // 客户端接收到3后,从FileData中加载到LocalPlayer并修改myPlayer.客户端状态1变为2(Hook点).
    // 随后发送4(玩家基础信息),68(UUID,无用),16(HP,并会修改dead状态),42(MP),50(Buff),5(Item),SyncPlayer(Mod Data),6. 状态由2变为3.
    // 服务端接收到6后,服务端状态1变为2.返回7(世界基础信息不带mod)并同步入侵事件.
    // 客户端接收7后,初始化世界信息(maxTiles,GameMode,ServerSideCharacter...),状态由3转4,当状态大于4时接收Mod Data;

    // 客户端发送8,请求图格数据.
    // 服务端接收到8后,服务端状态2变为3.
    // 随后发送9(加载状态),11(图格区块数据),21(掉落物),22(掉落物),23(NPC),27(弹幕),83(杀怪计数),57(世界类型),7(世界基础信息带mod),103,101,136,49


    // 按理来说需要开启Main.ServerSideCharacter,可以将Player.MarkAsServerSide();
    // 但客户端发送到服务端的数据,会在服务端重新分发时接收,原本并不需要接收.而且会造成创造模式的无限物品失效.
    // 总上,出于节省资源和接近单人模式的游戏体验,不会使用内置的SSC.