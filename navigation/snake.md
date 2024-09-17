<style>
    body{
        background-color: #111111; /* New background color */
    }
    .wrap{
        margin-left: auto;
        margin-right: auto;
    }

    canvas{
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF; /* Keep the wall color */
    }
    canvas:focus{
        outline: none;
    }

    /* All screens style */
    #gameover p, #setting p, #menu p{
        font-size: 20px;
        color: #FFDDC1; /* Text color change */
    }

    #gameover a, #setting a, #menu a{
        font-size: 30px;
        display: block;
        color: #FFDDC1; /* Link color change */
    }

    #gameover a:hover, #setting a:hover, #menu a:hover{
        cursor: pointer;
        color: #FF6F61; /* Hover color change */
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before{
        content: ">";
        margin-right: 10px;
    }

    #menu{
        display: block;
    }

    #gameover{
        display: none;
    }

    #setting{
        display: none;
    }

    #setting input{
        display:none;
    }

    #setting label{
        cursor: pointer;
        background-color: #FFDDC1;
        padding: 5px;
        margin: 5px;
        border-radius: 3px;
    }

    #setting input:checked + label{
        background-color: #FF6F61;
        color: #000;
    }
</style>

<div id="setting" class="py-4 text-light">
    <p>Speed:
        <input id="speed1" type="radio" name="speed" value="150" checked/>
        <label for="speed1">Slow</label>
        <input id="speed2" type="radio" name="speed" value="100"/>
        <label for="speed2">Normal</label>
        <input id="speed3" type="radio" name="speed" value="50"/>
        <label for="speed3">Fast</label>
        <input id="speed4" type="radio" name="speed" value="30"/>
        <label for="speed4">Super Fast</label>
        <input id="speed5" type="radio" name="speed" value="15"/>
        <label for="speed5">Ultra Fast</label>
    </p>
    <p>Wall:
        <input id="wallon" type="radio" name="wall" value="1" checked/>
        <label for="wallon">On</label>
        <input id="walloff" type="radio" name="wall" value="0"/>
        <label for="walloff">Off</label>
    </p>
</div>

<script>
    (function(){
        const canvas = document.getElementById("SASS");
        const ctx = canvas.getContext("2d");

        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");
        let SASS_speed;

        window.onload = function(){
            // speed
            setSASSSpeed(150);
            for(let i = 0; i < speed_setting.length; i++){
                speed_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < speed_setting.length; i++){
                        if(speed_setting[i].checked){
                            setSASSSpeed(speed_setting[i].value);
                        }
                    }
                });
            }
        }

        let setSASSSpeed = function(speed_value){
            SASS_speed = speed_value;
        }

        let activeDot = function(x, y){
            ctx.fillStyle = "#FFDDC1"; // New SASS and food color
            ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
        }

        let mainLoop = function(){
            // Repaint canvas
            ctx.beginPath();
            ctx.fillStyle = "#333333"; // New background color for canvas
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            // Paint SASS and food with updated color
            for(let i = 0; i < SASS.length; i++){
                activeDot(SASS[i].x, SASS[i].y);
            }
            activeDot(food.x, food.y);
            setTimeout(mainLoop, SASS_speed);
        }
    })();
</script>
