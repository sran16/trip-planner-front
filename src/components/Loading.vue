<script setup>

</script>
<template>
    <div class="row">
        <div class="span">
            <div class="location_indicator">
            </div>
        </div>
        <p>Votre itinéraire est en cours d'élaboration..</p>
    </div>
</template>
<style scoped>
* {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}


.row {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 10000;
    text-align: center;
    padding: 40vh 0px;
    background-color: #242321;
    display: flex;
    justify-content: center;
    flex-direction: column;
}

.span {
    width: 100vw;
    height: 15vh;
}

p {
    color: #6D695E;
    font-size: 1rem;
    font-weight: 200;
    font-family: 'inter', sans-serif;

}


/*Location indicator  icon */

.location_indicator {
    position: relative;
    z-index: 1;
    left: -22px;
}

.location_indicator:before,
.location_indicator:after {
    position: absolute;
    content: "";
}

.location_indicator:before {
    width: 50px;
    height: 50px;
    border-radius: 100% 100% 100% 0;
    box-shadow: 0px 0px 0px 2px rgba(255, 255, 255, 1);
    -webkit-animation: mapping 1s linear infinite;
    -moz-animation: mapping 1s linear infinite;
    animation: mapping 1s linear infinite;
    -webkit-transform: rotate(-46deg);
    -moz-transform: rotate(-46deg);
    transform: rotate(-46deg);
}

.location_indicator:after {
    width: 80px;
    height: 10px;
    border-radius: 100%;
    left: 46%;
    background-color: #6D695E;
    top: 9vh;
    z-index: -1;

}


@-webkit-keyframes mapping {
    0% {
        top: 0;
    }

    50% {
        top: -5px;
    }

    100% {
        top: 0;
    }
}

@-moz-keyframes mapping {
    0% {
        top: 0;
    }

    50% {
        top: -5px;
    }

    100% {
        top: 0;
    }
}

@-keyframes mapping {
    0% {
        top: 0;
    }

    50% {
        top: -5px;
    }

    100% {
        top: 0;
    }
}
</style>