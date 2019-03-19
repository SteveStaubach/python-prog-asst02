input.onGesture(Gesture.Shake, function () {
    control.reset()
})
let elazer: game.LedSprite = null
let enemy: game.LedSprite = null
let player: game.LedSprite = null
let lazer: game.LedSprite = null
music.beginMelody(music.builtInMelody(Melodies.PowerUp), MelodyOptions.OnceInBackground)
while (true) {
    if (input.buttonIsPressed(Button.AB)) {
        while (true) {
            enemy = game.createSprite(3, 0)
            player = game.createSprite(4, 4)
            basic.forever(function () {
                while (enemy.get(LedSpriteProperty.X) == player.get(LedSpriteProperty.X)) {

                    elazer = game.createSprite(enemy.get(LedSpriteProperty.X), enemy.get(LedSpriteProperty.Y))
                    for (let i = 0; i < 4; i++) {
                        elazer.change(LedSpriteProperty.Y, 1)
                        basic.pause(200)
                    }
                    if (elazer.get(LedSpriteProperty.X) == player.get(LedSpriteProperty.X) && elazer.get(LedSpriteProperty.Y) == player.get(LedSpriteProperty.Y)) {
                        music.playTone(80, music.beat(BeatFraction.Half))
                        music.beginMelody(music.builtInMelody(Melodies.Punchline), MelodyOptions.OnceInBackground)
                        game.gameOver()
                    }
                    if (elazer.get(LedSpriteProperty.Y) >= 4) {
                        elazer.delete()
                    }
                    basic.pause(1000)
                }
            })
            while (true) {
                input.onButtonPressed(Button.A, function () {
                    player.change(LedSpriteProperty.X, -1)
                })
                input.onButtonPressed(Button.B, function () {
                    player.change(LedSpriteProperty.X, 1)
                })
                input.onButtonPressed(Button.AB, function () {
                    lazer = game.createSprite(player.get(LedSpriteProperty.X), player.get(LedSpriteProperty.Y))
                    music.playTone(147, music.beat(BeatFraction.Sixteenth))
                    music.playTone(275, music.beat(BeatFraction.Sixteenth))
                    music.playTone(494, music.beat(BeatFraction.Sixteenth))
                    for (let j = 0; j < 4; j++) {
                        lazer.change(LedSpriteProperty.Y, -1)
                        basic.pause(100)
                        if (lazer.get(LedSpriteProperty.X) == enemy.get(LedSpriteProperty.X) && lazer.get(LedSpriteProperty.Y) == enemy.get(LedSpriteProperty.Y)) {
                            music.playTone(347, music.beat(BeatFraction.Eighth))
                            music.playTone(247, music.beat(BeatFraction.Eighth))
                            music.playTone(547, music.beat(BeatFraction.Eighth))
                            game.addScore(1)
                            enemy.set(LedSpriteProperty.Y, 0)
                        }
                    }
                    if (lazer.get(LedSpriteProperty.Y) <= 0) {
                        lazer.delete()
                    }
                })
                for (let i = 0; i < 4; i++) {
                    if (enemy.get(LedSpriteProperty.Y) == 4) {
                        music.beginMelody(music.builtInMelody(Melodies.Punchline), MelodyOptions.OnceInBackground)
                        game.gameOver()
                    }
                    for (let i = 0; i < 4; i++) {
                        enemy.change(LedSpriteProperty.X, -1)
                        basic.pause(200)
                    }
                    if (enemy.get(LedSpriteProperty.Y) == 4) {
                        music.beginMelody(music.builtInMelody(Melodies.Punchline), MelodyOptions.OnceInBackground)
                        game.gameOver()
                    }
                    for (let i = 0; i < 4; i++) {
                        enemy.change(LedSpriteProperty.X, 1)
                        basic.pause(200)
                    }
                }
                enemy.change(LedSpriteProperty.Y, 1)
                basic.pause(200)
            }
        }
    } else {
        basic.showString("BIT  BLASTER", 50)
    }
}
