<template>
    <div>
        <Nav />
        <br />
        <div  v-if="$store.state.cart.cart.length == 0" class="text-center">
<p>No items just yet</p></div>
<v-container>
        <div class="mb-3" v-if="$store.state.cart.cart.length > 0">
        <v-btn nuxt to="/cart" min-width="150" min-height="45" depressed>Back</v-btn>
        <v-btn @click="process" min-height="45" color="primary">Complete</v-btn>
        </div>
        <v-form lazy-validation ref="form" clss="mt-10">
            <p class="font-weight-bold" >Personal & Delivery</p>
            <v-row>
                <v-col cols="12" md="4">
                    <v-text-field v-model="email" :rules="[rules.required, rules.email]"
                    outlined label="Email" type="email"></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                    <v-text-field v-model="name" :rules="[rules.required]"
                    outlined label="Full Name" type="text"></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                    <v-text-field v-model="phone" outlined label="Phone" type="tel"></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                    <v-text-field v-model="address" :rules="[rules.required]"
                    outlined label="Address" type="text"></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                    <v-text-field v-model="city" :rules="[rules.required]"
                    outlined label="City" type="text"></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                    <v-text-field v-model="country" :rules="[rules.required]"
                    outlined label="Country" type="text"></v-text-field>
                </v-col>
            </v-row>
            <p class="font-weight-bold">Credit Card</p>
            <v-row>
                <v-cols cols="12" md="12">
                    <v-text-field v-model="ccv"
                    :rules="[rules.required]" outlined label="Credit Card Number"></v-text-field>
                </v-cols>
                <v-col cols="12" md="6">
                    <v-text-field v-model="expdate"
                    :rules="[rules.required]" outlined label="Exp Date"></v-text-field>
                </v-col>
                <v-col cols="12" md="6">
                    <v-text-field v-model="cvv"
                    :rules="[rules.required]" outlined label="Security Code/CVV"></v-text-field>
                </v-col>
            </v-row>
        </v-form>
    </v-container>
    </div>
</template>

<script>
export default {
    methods: {
        async process(){
            if(!this.$refs.form.validate()) return;
           await this.$swal({
            title: "Processing your order",
            icon: "info",
            allowEscapeKey: false,
            timer: 2000,
            timerProgressBar: true,
            text: "Please Wait",
            showConfirmButton: false,
           });

           await this.$swal({
            title: "Order Complete",
            icon: "success",
            allowEscapeKey: false,
            allowOutsideClick: false,
            timer: 3000,
            timerProgressBar: true,
            text: "Thanks for your Support",
            showConfirmButton: false,
           });
           this.$store.commit("cart/ClearCart");
           this.$router.push("/");

        },
    },
    data() {
        return {
            email: null,
            name: null,
            phone: null,
            address: null,
            city: null,
            country: null,
            cc: "424242424242",
            expdate: "06/15",
            cvv: "123",
            rules: {
                required: (v) =>  !!v  || "Required",
                email: (v)=> {
                    const pattern = /^[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$/;
                    return pattern.test(v) || 'Inavlid e-mail'
                }
            }
        };
    }
}
</script>

<style>

</style>