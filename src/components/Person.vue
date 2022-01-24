<template>
    <div>
        <h2 class="person__title">Person</h2>
        <div v-if="data">
            <img class="avatar" :src="data.avatar" alt="avatar">
            <p class="text"><span class="key">First Name:</span> {{ data.first_name }}</p>
            <p class="text"><span class="key">Last name:</span> {{ data.last_name }}</p>
            <p class="text"><span class="key">User name:</span> {{ data.username }}</p>
            <p class="text"><span class="key">Password:</span> {{ data.password }}</p>
            <p class="text"><span class="key">E-mail:</span> {{ data.email }}</p>
            <p class="text"><span class="key">Gender:</span> {{ data.gender }}</p>
            <p class="text"><span class="key">Phone number:</span> {{ data.phone_number }}</p>
            <p class="text"><span class="key">Social insurance number:</span> {{ data.social_insurance_number }}</p>
            <p class="text"><span class="key">Date of birth:</span> {{ data.date_of_birth }}</p>
            <p class="text"><span class="key">Employment:</span> {{ data.employment.title }}</p>
            <p class="text"><span class="key">Key skill:</span> {{ data.employment.key_skill }}</p>
            <ul class="person_list">
                <span class="key">Address:</span>
                <li class="text"><span class="key">City:</span> {{ data.address.city }}</li>
                <li class="text"><span class="key">Street name:</span> {{ data.address.street_name }}</li>
                <li class="text"><span class="key">Street address:</span> {{ data.address.street_address }}</li>
                <li class="text"><span class="key">Zip code:</span> {{ data.address.zip_code }}</li>
                <li class="text"><span class="key">State:</span> {{ data.address.state }}</li>
                <li class="text"><span class="key">Country:</span> {{ data.address.country }}</li>
            </ul>
            <p class="text"><span class="key">Credit card number:</span> {{ data.credit_card.cc_number }}</p>
            <ul class="person_list">
                <span class="key">Subscription:</span> 
                <li class="text"><span class="key">Plan:</span> {{ data.subscription.plan }}</li>
                <li class="text"><span class="key">Status:</span> {{ data.subscription.status }}</li>
                <li class="text"><span class="key">Payment method:</span> {{ data.subscription.payment_method }}</li>
                <li class="text"><span class="key">Term:</span> {{ data.subscription.term }}</li>
            </ul>
        </div>
        <p v-if="loading">Wait...</p>
        <p v-if="error">{{ error }}</p>
    </div>
</template>

<script>
import { onMounted, ref } from "vue"

export default {
    name: "Person",
    setup() {
        let data = ref(null);
        const loading = ref(true);
        const error = ref(null);

        function fetchData() {
            loading.value = true;

            return fetch("https://random-data-api.com/api/users/random_user", {
                method: "get",
                headers: {
                    "content-type": "application/json"
                }
            })
                .then(res => {
                    if (!res.ok) {
                        const error = new Error(res.statusText);
                        error.json = res.json();
                        throw error;
                    }

                    return res.json();
                })
                .then(json => {
                    data.value = json;
                })
                .catch(err => {
                    error.value = err;
                    if (err.json) {
                        return err.json.then(json => {
                            error.value.message = json.message;
                        });
                    }
                })
                .then(() => {
                    loading.value = false;
                });
        }

        onMounted(() => {
            fetchData();
        });

        return {
            data,
            loading,
            error
        };
    }

}
</script>