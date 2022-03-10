<template>
    <header>
        <div class="dropdown" style="float:right;">
            <label class="cart--label grey"><a class="dropdown--button">My Cart({{cartLength}})</a></label>
            <div class="dropdown--content">
                <div class="cart--container"  v-for="item in pr.cartContent" :key=item.size>
                    <img class="cart--image" 
                            src="../assets/classic-tee.jpg" 
                            alt="product image"/>
                    <div class="dropdown--cart">
                        <label class="black"> 
                            {{item.title}}
                        </label>
                        <label class="black"> 
                            <b> {{item.quantity}}x ${{item.price}} </b>
                        </label>
                        <label class="label--size grey"> 
                            Size: <span class="black">{{item.size}}</span>
                        </label>
                    </div>
                </div>
            </div>
        </div>
    </header>
    <section>
        <div class="main--container">
            <div class="image--container">
                <img class="product--image" 
                        src="../assets/classic-tee.jpg" 
                        alt="product image"/>
            </div>
            <div class="label--container">
                <label class="label--title black"> 
                    {{Constants.product_title}}
                </label>
                <div class="border--line"></div>
                <label class="label--price black"> 
                    <b> ${{Constants.product_price}} </b>
                </label>
                <div class="border--line"></div>
                <label class="label--description grey"> 
                    {{Constants.product_description}}
                </label>
                <label class="label--size grey"> 
                    SIZE
                    <span class="red">*</span>
                    <span class="black">{{pr.sizeSelected}}</span>
                    
                </label>
                <div class="size--container">
                    <button class="button" :class="pr.smallSelected  ? 'black solid' : 'light__grey light'" v-on:click="selectHandler('S')">S</button>
                    <button class="button" :class="pr.mediumSelected ? 'black solid' : 'light__grey light'" v-on:click="selectHandler('M')">M</button>
                    <button class="button" :class="pr.largeSelected  ? 'black solid' : 'light__grey light'" v-on:click="selectHandler('L')">L</button>
                </div>
                <button class="add__cart button solid black" v-on:click="addToCart">ADD TO CART</button>
            </div>
        </div>
    </section>
    <footer>
        <div class="nav--container">
        </div>
    </footer>
</template>

<script>

import { Constants }    from '../constants'

export default {
    data() {
      return {
          Constants: Constants,
            pr: {
                smallSelected   : true,
                mediumSelected  : false,
                largeSelected   : false,
                sizeSelected    : 'S',
                cartContent     : []
            }
        }
    },

    computed: {
        cartLength() {
            let ref = this;
            let totalItems = 0;

            ref.pr.cartContent.forEach(item => {
                totalItems = totalItems + item.quantity;
            });

            return totalItems;
        }
    },

    mounted() {
    },

    methods: {
        selectHandler(item) {
            let ref = this;

            ref.pr.smallSelected    = false;
            ref.pr.mediumSelected   = false;
            ref.pr.largeSelected    = false;
            ref.pr.sizeSelected     = item;

            if(item == 'S') {
                ref.pr.smallSelected    = !ref.pr.smallSelected;
            } else if(item == 'M') {
                ref.pr.mediumSelected   = !ref.pr.mediumSelected;
            } else if(item == 'L') {
                ref.pr.largeSelected    = !ref.pr.largeSelected;
            }
        },

        addToCart() {
            let ref = this;
            let isExisting = ref.pr.cartContent.find(item => item.size == ref.pr.sizeSelected);

            if(isExisting) {
                let index = ref.pr.cartContent.findIndex(item => item.size == ref.pr.sizeSelected);

                isExisting.quantity = isExisting.quantity + 1;
                isExisting.price    = isExisting.price *  isExisting.quantity;

                ref.pr.cartContent[index] = isExisting;
            } else {
                let item = {
                    title       : Constants.product_title,
                    price       : Constants.product_price,
                    size        : ref.pr.sizeSelected,
                    quantity    : 1
                }

                ref.pr.cartContent.push(item);
            }
        }
    },
}
</script>

<style scoped>

    header {
        height: 2rem;
        width: 100%;
        justify-content: flex-end;
        align-items: center;
        display: flex;
        background-color: #F6F6F7;
        padding: 0 2rem;
        margin-top: 1rem;
    }

    /* CART DROPDOWN */
    .cart--label {
        top: 5rem;
    }

    .dropdown--cart {
        display: inherit;
        flex-direction: column;
        width: 10vh;
        gap: 0.3rem;
    }

    .dropdown--button {
        cursor:pointer;
    }

    .dropdown {
        position: relative;
        display: inline-block;
    }

    .dropdown--content {
        display: none;
        position: absolute;
        background-color: #f1f1f1;
        right: 0;
        min-width: 300px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 1;
    }

    .dropdown--content a {
        color: black;
        padding: 12px 16px;
        text-decoration: none;
        display: block;
    }

    .dropdown--content a:hover {
        background-color: white;
    }

    .cart--container {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        gap: 1rem;
    }

    .dropdown:hover .dropdown--content {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        gap: 1rem;
        padding: 1rem;
        background-color: white;
    }

    .dropdown:hover .dropdown--button {
        background-color: white;
    }
    
    section {
        width: 100%;
        display: flex;  
        align-content: center;
        align-items: center;
        justify-content: center;
    }

    footer {
        display: flex;
        width: 100%;
        flex-direction: row-reverse;
        padding-right: 2rem;
    }
   
    .main--container {
        height: 100%;
        width: 80%;
        display: flex;
        flex-flow: wrap row; 
        justify-content: center;
        gap: 10rem;    
    }

    /* IMAGE */
    .image--container {
		width: 40vh;
    }

    .cart--image {
        width: 10vh;
    }

    .product--image {
        width: 100%
    }
    
    .border--line {
        border-bottom: 0.2px #CCCCCC solid;
    }

    /* LABELS */
    .label--container {
        display: inherit;
        flex-direction: column;
        width: 50vh;
        gap: 1rem;
    }

    .label--title {
        font-weight: 700;
        font-size: 1.3rem;
    }

    .label--price {
        font-weight: 900;;
    }

    .label--size {
        display: inherit;
        gap: 5px;
    }

    .grey {
        color: #888888;
    }

    .light__grey {
        color: #CCCCCC;
    }

    .black {
        color: #222222;
    }

    .red {
        color:#C90000;
    }
    
    .required:before {
        content:" *";
        color: red;
    }

    /* BUTTONS */
    .size--container {
        display: inherit;
        flex-direction: row;
        gap: 0.5rem;
    }

    .button {
        background-color: transparent;
        padding: 10px 15px;
        text-align: center;
        font-size: 0.8rem;
        font-weight: 500;
        cursor: pointer;
    }

    .add__cart {
        font-weight: 700;
        width: 20vh;
    }

    .light {
        border: 2px solid #CCCCCC;
    }

    .solid {
        border: 2px solid #222222;
    }
</style>