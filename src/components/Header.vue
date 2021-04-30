<template>
    <header>
        <div class="container">
            <div class="header">
                <div class="logo__header logo">
                    <img src="../assets/images/StarWars.png" alt="">
                </div>
                <div class="menu">
                    <div class="menu__lang">
                        <div>EN</div>
                        <img class="arrow" src="~@/assets/images/Shape.png" alt="">
                    </div>
                    <div class="menu__logIn">Log in</div>
                    <div class="menu__signUp btn">Sign up</div>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style scoped lang="scss">
    header {
        flex: 0 0 auto;
    }
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        max-height: 80px;

        .logo__header {
            margin: 24.3px 0 25.3px;
        }
        .menu {
            font-size: 14px;

            &__lang {
                display: flex;
                align-items: center;

                div + img {
                    margin-left: 7px;
                }
            }
            &__logIn {
                margin-left: 62px;
            }
            &__signUp {
                margin-left: 43px;
                padding: 16px 56px;
                color: white;
            }
        }
    }

    @media (max-width: 480px) {
        #app header {
            background: white;
        }
        .header {
            .menu__logIn {
                display: none;
            }

            .menu__lang {
                display: none;
            }

            .menu__signUp {
                background-color: white !important;
                color: black;
                position: relative;

                &:before {
                    position: absolute;
                    right: 0;
                    top: calc(50% - 1.3px / 2 - 5.85px);
                    content: '';
                    display: block;
                    height: 1.3px;
                    background: black;
                    width: 24px;
                }

                &:after {
                    position: absolute;
                    right: 0;
                    top: calc(50% - 1.3px / 2 + 5.85px);
                    content: '';
                    display: block;
                    height: 1.3px;
                    background: black;
                    width: 24px;
                }
            }
        }
    }

</style>