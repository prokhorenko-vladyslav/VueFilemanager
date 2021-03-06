<template>
    <div class="modal__window" :class="{active : isActive}" @keyup.prevent.enter="submitModal">
        <div class="modal__backdrop" @click="closeModal"></div>
        <div class="modal">
            <div class="modal__title">
                <slot name="header"></slot>
            </div>
            <div class="modal__body">
                <slot name="body"></slot>
            </div>
            <div class="modal__buttons">
                <div class="modal__button modal__button_submit" @click="submitModal">Submit</div>
                <div class="modal__button modal__button_cancel" @click="closeModal">Cancel</div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ModalComponent",
        props: {
            active: {
                default : false
            }
        },
        data() {
          return {
              isActive : this.active
          }
        },
        watch: {
            active() {
              this.isActive = this.active;
            }
        },
        methods: {
            submitModal() {
                this.$emit('modal-submit');
            },
            closeModal() {
                this.$emit('modal-close');
            }
        }
    }
</script>

<style lang="scss" scoped>
    .modal__window {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;

        .modal__backdrop {
            position: absolute;
            right: 0;
            top: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            background: rgba(0,0,0,.35);
            transition: all .3s ease-in-out;
            pointer-events: none;
        }

        .modal {
            position: relative;
            bottom: -100%;
            width: 700px;
            height: auto;
            overflow-y: auto;
            border-radius: .5rem;
            box-shadow: -8px 0 18px 0 rgba(25,42,70,.13);
            background: #fff;
            transition: all .3s ease-in-out;
            z-index: 10;

            .modal__title {
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 1rem;
                border-bottom: 1px solid #EDEDED;
                font-size: 1.2rem;
            }

            .modal__body {
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 1rem;

                .modal__errors {
                    .modal__error {
                        color: rgba(217, 34, 34, 0.8);
                    }
                }

                .modal__section {
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    flex-wrap: wrap;
                    width: 100%;

                    &.half {
                        width: 50%;
                        margin-right: 1rem;
                        padding-left: 1rem;
                        padding-right: 1rem;
                        border-right: 1px solid #DFE3E7;

                        &:last-of-type {
                            margin-right: 0;
                            border-right: 0;
                        }
                    }

                    .modal__header {
                        width: 100%;
                        display: flex;
                        justify-content: center;
                        margin-bottom: 1rem;

                        .modal__header__item {
                            width: 50%;
                            display: flex;
                            justify-content: center;
                            font-size: 1.2rem;
                        }
                    }

                    .modal__label {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        width: 100%;
                        margin-bottom: 1rem;

                        &.modal__label_file {
                            .modal__text {
                                display: flex;
                                justify-content: center;
                                align-items: center;
                                width: 100%;
                                height: 200px;
                                margin: 1rem;
                                border: 2px dashed #5A8DEE;
                                font-size: 1.5rem;
                                font-style: italic;
                                animation: pulse 2s ease-in-out infinite;
                                cursor: pointer;
                                transition: all .3s ease-in-out;
                                
                                &:hover {
                                    box-shadow: 0 0 6px 0 rgba(90,141,238,.6);
                                }
                            }

                            .modal__file {
                                display: none;
                            }
                        }

                        .modal__text {
                            width: 50%;
                            display: flex;
                            justify-content: center;
                        }

                        .modal__input {
                            width: 50%;

                            label {
                                width: auto;
                            }
                        }
                    }

                    .modal__input__wrapper {
                        width: 50%;
                        margin-top: 1rem;
                        margin-bottom: 1rem;

                        .modal__input {
                            width: 100%;
                            border: none;
                            border-bottom: 1px solid #DFE3E7;
                            transition: all .3s ease-in-out;

                            &.error {
                                border-bottom: 1px solid rgba(217, 34, 34, 0.6);
                            }
                        }
                    }
                }
            }

            .modal__buttons {
                display: flex;
                justify-content: center;
                align-items: center;
                padding-top: 1rem;
                padding-bottom: 1rem;
                border-top: 1px solid #EDEDED;

                .modal__button {
                    margin-left: 1rem;
                    margin-right: 1rem;
                    padding: .2rem 1rem;
                    box-shadow: 0 0 12px 0 rgba(90,141,238,.3);
                    border: 1px solid transparent;
                    border-radius: .25rem;
                    color: #fff;
                    font-size: 1rem;
                    opacity: .8;
                    cursor: pointer;
                    user-select: none;
                    transition: all .3s ease-in-out;

                    &:hover {
                        box-shadow: 0 0 12px 0 rgba(90,141,238,.6);
                        opacity: 1;
                    }

                    &.modal__button_submit {
                        background: rgba(72,180,127,.8);
                    }

                    &.modal__button_cancel {
                        background: rgba(217, 34, 34, 0.8);
                    }
                }
            }
        }

        &, * {
            pointer-events: none;
        }

        &.active {
            &, * {
                pointer-events: all;
            }

            .modal {
                bottom: 0;
            }

            .modal__backdrop {
                opacity: 1;
            }
        }
    }

    @keyframes pulse {
        0% {
            box-shadow: 0 0 8px 0 rgba(90, 141, 238, 0);
        }

        50% {
            box-shadow: 0 0 8px 0 rgba(90, 141, 238, 0.8);
        }

        100% {
            box-shadow: 0 0 8px 0 rgba(90, 141, 238, 0);
        }
    }
</style>