<script setup>
</script>
<template>
    <div class="row ">
        <div class="span">
            <div class="location_indicator">
            </div>
        </div>
    </div>
</template>
<style scoped>
* {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}


.row {
    position: absolute;
    top: 0;
    text-align: center;
    padding: 10px 0;
    background-color: #242321;
    display: flex;
    justify-content: center;
    align-items: center;

}

.span {
    width: 100vw;
    height: 15vh;
    padding: 50vh 0;
}


/*Location indicator */
.location_indicator {
    position: relative;
    z-index: 1;
    left: -9px;
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