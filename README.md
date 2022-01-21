# Cristalix Arcade API DOCS (актуальная версия 1.0.23)

Это система объединяющая все аркады на Cristalix. 
Проект тянет за собой Animation API, и сам включает его, поэтому вам не нужно добавлять его отдельно.
Мультисерверные: валюта, префикс, лутбосы, донат, достижения (скоро)
<br>

<h2>Gradle Get Started</h2>

```
repositories {
  mavenLocal()
  mavenCentral()
  maven {
    url 'https://repo.implario.dev/cristalix/'
    credentials {
      username System.getenv("IMPLARIO_REPO_USER")
      password System.getenv("IMPLARIO_REPO_PASSWORD")
    }
  }
}

dependencies {
  implementation 'me.func:arcade-api:1.0.23'
  implementation 'org.jetbrains.kotlin:kotlin-stdlib:1.6.0'
}
```

<h2>Важно</h2>

При начале игры нужно вызвать (если вы используете games5e укажите в скобках реалм) `Arcade.start()`<br>
При завершении игры или при кике всех игроков нужно вызвать `Arcade.bulkSave(vararg players: Player)` чтобы сделать сохранение игроков в одном запросе, а не в отдельных

<h2>Методы</h2>

<h3>Основное</h3> 

`Arcade.getMoney(uuid: UUID)` получить баланс игрока по UUID<br>
`Arcade.getMoney(player: Player)` получить баланс по игроку<br>
<br>
`Arcade.setMoney(uuid: UUID, money: Long)` поставить баланс по UUID<br>
`Arcade.setMoney(player: Player, money: Long)` поставить баланс<br>
<br>
`Arcade.deposit(uuid: UUID, money: Int)` выдать игроку деньги по UUID (с сообщением на экране)<br>
`Arcade.deposit(player: Player, money: Int)` выдать игроку деньги<br>
<br>
`Arcade.openLootbox(uuid: UUID)` убрать игроку один лутбокс<br>
`Arcade.giveLootbox(uuid: UUID)` выдать игроку один лутбокс<br>
<br>
`Arcade.updatePrefix(uuid: UUID, prefix: String)` обновить мультисерверный префикс <br>


<h3>Музыка</h3>

`Music.EXPLOSION.sound(vararg player: Player)` проигрывание звука взрыва<br>
`Music.RARE_ITEM.sound(vararg player: Player)` звук редкого предмета<br>
`Music.LEVEL_UP.sound(vararg player: Player)` звук улучшения уровня<br>
`Music.LEVEL_UP2.sound(vararg player: Player)` второй звук улучшения уровня<br>
`Music.BONUS.sound(vararg player: Player)` звук поднятия бонуса<br>
`Music.BONUS2.sound(vararg player: Player)` другой звук поднятия бонуса<br>

`Music.sound(source: String, vararg player: Player)` проигрывание звука по прямой ссылке на звук<br>
`Music.stop(vararg player: Player)` прекращение проигрывание звука<br>

<h3>Дополнительное</h3>

`Arcade.getDonate(uuid: UUID): ArcadePlayer` получить весь донат игрока по UUID<br>
`Arcade.getDonate(player: Player): ArcadePlayer` получить весь донат игрока<br>

`SkullManager.create(URL: String?): ItemStack` возвращает вам голову игрока со скином указанным по URL<br>
`Firework.generate(location: Location, vararg colors: Color)` создает фейрверки нужных цветов на указанной локации<br>

<h3>Весь донат</h3>

```
    var killMessage: KillMessage = KillMessage.NONE, // сообщения при убийстве
    var stepParticle: StepParticle = StepParticle.NONE, // частицы ходьбы
    var nameTag: NameTag = NameTag.NONE, // префикс
    var corpse: Corpse = Corpse.NONE, // магила после смерти
    var arrowParticle: ArrowParticle = ArrowParticle.NONE, // частицы стрелы
    var mask: Mask = Mask.NONE, // маска на голову
```
