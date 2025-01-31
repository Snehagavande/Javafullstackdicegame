# Javafullstackdicegame
# Java Full Stack Dice Game

This is a simple full-stack dice game built with Java (Spring Boot) for the backend and HTML, CSS, and JavaScript for the frontend.

## Features
- Players can input their names.
- Click "Roll Dice" to simulate rolling the dice.
- Displays the result of the dice roll.

## Backend
The backend is built using Spring Boot and provides an API endpoint to simulate dice rolls.
package com.dicegame;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DiceGameApplication {

    public static void main(String[] args) {
        SpringApplication.run(DiceGameApplication.class, args);
    }
}
##DiceController.java
package com.dicegame.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.Random;

@RestController
public class DiceController {

    private final Random random = new Random();

    @GetMapping("/rollDice")
    public String rollDice(@RequestParam(value = "player", defaultValue = "Player") String playerName) {
        int roll = random.nextInt(6) + 1;
        return playerName + " rolled a " + roll;
    }
}


## Frontend
The frontend is a simple HTML page that makes an API call to the backend to fetch the dice roll result.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
        }
        .container {
            margin-top: 50px;
        }
        .input-group {
            margin: 10px;
        }
        input {
            padding: 10px;
            margin: 5px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
        .result {
            font-size: 20px;
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Java Dice Game</h1>
        <div class="input-group">
            <input type="text" id="player1" placeholder="Player 1 Name">
            <input type="text" id="player2" placeholder="Player 2 Name">
        </div>
        <button onclick="rollDice()">Roll Dice</button>

        <div id="result" class="result"></div>
    </div>

    <script>
        function rollDice() {
            const player1 = document.getElementById("player1").value || "Player 1";
            const player2 = document.getElementById("player2").value || "Player 2";

            fetch(`http://localhost:8080/rollDice?player=${player1}`)
                .then(response => response.text())
                .then(data => {
                    document.getElementById("result").innerHTML = data;
                });
        }
    </script>

</body>
</html>


## Run the Application

### Backend
1. Clone the repository.
2. Navigate to the `backend` folder and run the Spring Boot application:

```bash
mvn spring-boot:run
DiceGameApplication.java (Main Application Class)
package com.dicegame;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DiceGameApplication {

    public static void main(String[] args) {
        SpringApplication.run(DiceGameApplication.class, args);
    }
}

