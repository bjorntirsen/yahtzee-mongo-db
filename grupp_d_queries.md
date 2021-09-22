//OBS alla ObjectId måste ändras vid testning

//Skapa spelare (när man loggar in första gången)

db.player.insert({
    "name": "Niklas", 
    "email": "niklas@pellefant.se", 
    "games_played": 0,
    "games_won": 0,
    "personal_best": 0
});

//För att starta ett spel

db.game.insert({
    start_timedate: new Date(),
    no_of_players: 2, 
    players: [
        {player: 1, player_id: ObjectId("60229075b284761ca8ca1fe2")},
        {player: 2, player_id: ObjectId("6024f7799b89cb09c7596e05")},
    ],
    end_timedate: null,
    winning_player_id: null
})

//och detta för varje spelare i matchen

db.player_column.insert({
    game:  ObjectId("6024f7d09b89cb09c7596e06"), 
    player: ObjectId("60242d09b284761ca8ca1ff2"), 
    "fields": [
        { field: "ones", value: null },
        { field: "twos", value: null },
        { field: "threes", value: null },
        { field: "fours", value: null },
        { field: "fives", value: null },
        { field: "sixes", value: null },
        { field: "bonus", value: null },
        { field: "pairs", value: null },
        { field: "two_pairs", value: null },
        { field: "three_of_a_kind", value: null },
        { field: "four_of_a_kind", value: null },
        { field: "small_straight", value: null },
        { field: "large_straight", value: null },
        { field: "full_house", value: null },
        { field: "chance", value: null },
        { field: "yahtzee", value: null }
    ],
    total: null
})

//När en spelare sparar ett resultat tex: 3 i ettor

db.player_column.updateOne(
    {
        $and: [
            {game: ObjectId("6024f7d09b89cb09c7596e06")}, 
            {player: ObjectId("60242d09b284761ca8ca1ff2")}
        ]
    },
    {
        $set: {
            "fields.0.value": 3
        }
})

//När spelet är slut

//1: Sätta total score

db.player_column.updateOne(
    {
        $and: [
            {game: ObjectId("6024f7d09b89cb09c7596e06")}, 
            {player: ObjectId("60242d09b284761ca8ca1ff2")}
        ]
    },
    {
        $set: {
            "total": 140
        }
})

//2: Sätta sluttid

db.game.update({ _id: ObjectId("60242d46b284761ca8ca1ff3") }, {$set:{"end_timedate": new Date()}})

//3: Uppdatera alla games played

//3a: Vilka spelade?

db.player_column.find({ game: ObjectId("6024f7d09b89cb09c7596e06") }, {player:1, _id:0})

//3b: Uppdatera

db.player.update({_id: ObjectId("60229075b284761ca8ca1fe2")}, { $inc: { "games_played": 1} })

//4: Öka games won

//4a: Vem vann?

db.player_column.find({ game: ObjectId("6024f7d09b89cb09c7596e06") }, {player:1, _id:0}).sort({total:-1}).limit(1)

//4b: Uppdatera i player

db.player.update({_id: ObjectId("60242d09b284761ca8ca1ff2")}, { $inc: { "games_won": 1} })

//4c: Sätta winning_player i game

db.game.update({_id: ObjectId("6024f7d09b89cb09c7596e06")}, { $set: { winning_player_id: ObjectId("60242d09b284761ca8ca1ff2")} })

//Övriga frågor:

//Hur många poäng varje användare har fått i en match

db.player_column.find({ game: ObjectId("6024f7d09b89cb09c7596e06") }, {player:1, _id:0, total:1})

//Hur topplistan ser ut. Vår top_five collection innehåller max 5 dokument

db.top_five.find({},{player_name:1, placement:1, _id:0, games_won:1}).sort({placement:1})

//Hur många matcher en spelare har spelat

db.player.find({email: "niklas@pellefant.se"}, {name:1, games_played:1})

//Bortkommenterade färdiga spelexempel om man önskar

/* db.player_column.insert({
    game: ObjectId('6023f794b284761ca8ca1fed'),
    player: ObjectId('60229075b284761ca8ca1fe2'), 
    "fields": [
        { field: "ones", value: 3 },
        { field: "twos", value: 6 },
        { field: "threes", value: 6 },
        { field: "fours", value: 12 },
        { field: "fives", value: 10 },
        { field: "sixes", value: 18 },
        { field: "bonus", value: 0 },
        { field: "pairs", value: 8 },
        { field: "two_pairs", value: 6 },
        { field: "three_of_a_kind", value: 9 },
        { field: "four_of_a_kind", value: 4 },
        { field: "small_straight", value: 15 },
        { field: "large_straight", value: 20 },
        { field: "full_house", value: 28 },
        { field: "chance", value: 30 },
        { field: "yahtzee", value: 50 }
    ],
    total: 225
}) */

/* db.player_column.insert({
    game: ObjectId('602410b6b284761ca8ca1fef'),
    player: ObjectId('60229075b284761ca8ca1fe3'), 
    "fields": [
        { field: "ones", value: 3 },
        { field: "twos", value: 6 },
        { field: "threes", value: 12 },
        { field: "fours", value: 12 },
        { field: "fives", value: 10 },
        { field: "sixes", value: 18 },
        { field: "bonus", value: 60 },
        { field: "pairs", value: 4 },
        { field: "two_pairs", value: 8 },
        { field: "three_of_a_kind", value: 12 },
        { field: "four_of_a_kind", value: 12 },
        { field: "small_straight", value: 15 },
        { field: "large_straight", value: 20 },
        { field: "full_house", value: 28 },
        { field: "chance", value: 28 },
        { field: "yahtzee", value: 50 }
    ],
    total: 237
}) */