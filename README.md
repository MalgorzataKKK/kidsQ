<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dodawanie Quiz dla dzieci</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #6fdde295;
            padding: 20px;
        }

        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }


        .dzialanie {
            background-color: rgba(70, 131, 223, 0.773);
            height: 200px;
            width: 400px;
            font-size: 150px;
            text-align: center;
            line-height: 200px;
            border: 2px solid #000;
            margin: 30px auto;
            border: none;
            border-radius: 5px;
            place-items: center;
        }

        button {
            color: white;
            padding: 30px;
            font-size: 80px;
            width: 280px;
            height: 150px;
            margin: 3px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .czerwony {
            background-color: red;
        }

        .czerwony:hover {
            background-color: darkred;
        }

        .zielony {
            background-color: rgb(62, 221, 53);
        }

        .zielony:hover {
            background-color: green;
        }

        .pomaranczowy {
            background-color: orange;
        }

        .pomaranczowy:hover {
            background-color: rgb(221, 135, 31);
        }

        .fioletowy {
            background-color: rgb(174, 60, 192);
        }

        .fioletowy:hover {
            background-color: rgb(114, 36, 153);
        }

        #overlay {
            position: fixed;
            /* Sit on top of the page content */
            display: none;
            /* Hidden by default */
            width: 100%;
            /* Full width (cover the whole page) */
            height: 100%;
            /* Full height (cover the whole page) */
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            /* Black background with opacity */
            z-index: 2;
            /* Specify a stack order in case you're using a different order for other elements */
            cursor: pointer;
            /* Add a pointer on hover */
        }

        .obraz {
            max-width: 50%;
            max-height: 50%;
            margin: 25%
        }
    </style>
</head>

<body>

    <h1>MINI QUIZ DODAWANIE</h1>
    <div id="dzialanie" class="dzialanie">2+3</div>


    <div>
        <button id="przycisk_czerwony" class="czerwony">4</button>
        <button id="przycisk_zielony" class="zielony">5</button>
        <button id="przycisk_pomaranczowy" class="pomaranczowy">7</button>
        <button id="przycisk_fioletowy" class="fioletowy">9</button>
    </div>

    <div id="wynikDiv"></div>
    <div id="overlay">
        <img class="obraz" src="https://cdn.pixabay.com/photo/2016/03/31/14/37/check-mark-1292787_1280.png"
            alt="Obraz" />
    </div>

    <script>
        const dzialania = [
            {
                "dzialanie": "2+3",
                "a": "4",
                "b": "5",
                "c": "7",
                "d": "9",
                "poprawna": "b"
            },
            {
                "dzialanie": "4+4",
                "a": "6",
                "b": "9",
                "c": "8",
                "d": "10",
                "poprawna": "c"

            },
            {
                "dzialanie": "7 + 2",
                "a": "3",
                "b": "9",
                "c": "10",
                "d": "12",
                "poprawna": "b"

            },
            {
                "dzialanie": "5 + 3",
                "a": "2",
                "b": "6",
                "c": "8",
                "d": "10",
                "poprawna": "c"
            },
            {
                "dzialanie": "1 + 9",
                "a": "5",
                "b": "7",
                "c": "9",
                "d": "10",
                "poprawna": "d"

            },
            {
                "dzialanie": "2 + 4",
                "a": "6",
                "b": "5",
                "c": "8",
                "d": "9",
                "poprawna": "a"
            },
            {
                "dzialanie": "3 + 1",
                "a": "4",
                "b": "5",
                "c": "8",
                "d": "9",
                "poprawna": "a"
            },
            {
                "dzialanie": "8 + 4",
                "a": "9",
                "b": "11",
                "c": "12",
                "d": "14",
                "poprawna": "c"
            },
        ]

        document.getElementById('przycisk_czerwony').addEventListener('click', function (a) {

            sprawdź_Odpowiedź("a");
        });
        document.getElementById('przycisk_zielony').addEventListener('click', function (b) {
            sprawdź_Odpowiedź("b");
        });

        document.getElementById('przycisk_pomaranczowy').addEventListener('click', function (c) {
            sprawdź_Odpowiedź("c");
        });
        document.getElementById('przycisk_fioletowy').addEventListener('click', function (d) {
            sprawdź_Odpowiedź("d");
        });


        let obecne_pytanie = 0;
        function ustaw_pytanie(i) {
            const dzialanie = dzialania[i]
            document.getElementById("dzialanie").innerHTML = dzialanie.dzialanie
            document.getElementById("przycisk_czerwony").innerHTML = dzialanie.a
            document.getElementById("przycisk_zielony").innerHTML = dzialanie.b
            document.getElementById("przycisk_pomaranczowy").innerHTML = dzialanie.c
            document.getElementById("przycisk_fioletowy").innerHTML = dzialanie.d
            document.getElementById("wynikDiv").innerHTML = ""
        }
        ustaw_pytanie(0)

        function sprawdź_Odpowiedź(numer_odpowiedzi) {
            if (numer_odpowiedzi == dzialania[obecne_pytanie].poprawna) {

                wynikDiv.innerHTML = '✔ Dobrze!';
                on();
                obecne_pytanie = obecne_pytanie + 1;
                setTimeout(() => {
                    off();
                    if (obecne_pytanie < dzialania.length) {
                        ustaw_pytanie(obecne_pytanie);
                    } else {
                        wynikDiv.innerHTML = 'Koniec quizu!';
                        document.getElementById('dzialania').innerHTML = '';
                    }
                }, 2000); // Czekaj 4 sekundy przed przejściem do następnego pytania
            } else {
                wynikDiv.innerHTML = '❌ Spróbuj ponownie.';
            }
        }

        function on() {
            document.getElementById("overlay").style.display = "block";
        }

        function off() {
            document.getElementById("overlay").style.display = "none";
        }
    </script>

</body>

</html>
