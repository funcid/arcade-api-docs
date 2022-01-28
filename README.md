# Cristalix Arcade API DOCS

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
  implementation 'me.func:arcade-api:1.0.97'
  implementation 'org.jetbrains.kotlin:kotlin-stdlib:1.6.0'
}
```

<h2>Важно</h2>

При загрузке плагина нужно один раз вызвать (если вы используете games5e укажите в скобках реалм, для подключения к система BattlePass, укажите через запятую `ArcadeType` вашего режима) `Arcade.start()`<br>
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

<h3>Работа с BattlePass</h3> 

Квесты игрока случайно генерируются каждые N часов из определенного списка, чтобы обновлять прогресс игрока используйте `BattlePassUtil.update(player, questType, value, absolute)`, player - игрок, questType `KILL, WIN, PLAY, TIME, POINTS, BREAK, PLACE, DAMAGE`, value - если absolute, то число прогресс заменится на это значение, иначе просто добавится.<br>
Пример:
При убийстве игрока - `BattlePassUtil.update(damager, KILL, 1, false)`, если у игрока есть данный квест, то ему добавится одно убийство.

<h3>Музыка</h3>

Готовы звуки:
```
EXPLOSION("https://implario.dev/arcade/music/EXPLOSION.mp3"),
RARE_ITEM("https://implario.dev/arcade/music/RARE_ITEM.mp3"),
BONUS("https://implario.dev/arcade/music/BONUS.mp3"),
BONUS2("https://implario.dev/arcade/music/SECOND_BONUS.mp3"),
LEVEL_UP("https://implario.dev/arcade/music/LEVEL_UP.mp3"),
LEVEL_UP2("https://implario.dev/arcade/music/SECOND_LEVEL_UP.mp3"),
```

`Music.МУЗЫКА.sound(vararg player: Player)` включить игрокам готового звука<br>
`Music.sound(source: String, vararg player: Player)` проигрывание звука по прямой ссылке на звук<br>
`Music.stop(vararg player: Player)` прекращение проигрывание звука<br>

<h3>Дополнительное</h3>

`Arcade.getArcadeData(uuid: UUID): ArcadePlayer` получить весь донат игрока по UUID<br>
`Arcade.getArcadeData(player: Player): ArcadePlayer` получить весь донат игрока<br>

`Arcade.enableStepParticles()` включить частицы при ходьбе (не работает у `SPECTATOR`)<br>
`Arcade.enableArrowParticles()` включить частицы стрелы<br>
`Arcade.distributeLootbox(vararg player: Player)` дать шанс игрокам (передавайте только победителей) получить лутбокс.<br>

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
