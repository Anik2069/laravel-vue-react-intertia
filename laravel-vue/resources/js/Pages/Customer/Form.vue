<script setup lang="ts">
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';

defineProps({

    customer: {
        type: Array,
    },
});

const form = useForm({
    name: '',
    phone: '',
});


const submit = () => {
    form.post(route('customer.store'), {
        onFinish: () => form.reset(),
    });

};

const deleteCustomer = (customer) => {

    form.delete(route('customer.destroy', customer.id), {
        onSuccess: () => console.log(`${customer.name} deleted`),
    });
}
</script>



<template>
    <h2 class="text-xl font-semibold leading-tight text-gray-800 dark:text-gray-200">
        Customer Form
    </h2>
    <div class="grid  justify-center mx-auto">
        <div class="grid grid-cols-4 ">
            <form @submit.prevent="submit" class="w-full">
                <InputLabel for="name" value="name" />
                <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" required
                    autocomplete="current-password" autofocus />
                <InputLabel for="phone" value="Phone" />
                <TextInput id="phone" type="text" class="mt-1 block w-full" v-model="form.phone" required
                    autocomplete="current-password" autofocus />
                <PrimaryButton>Save</PrimaryButton>
            </form>
        </div>
    </div>
    <div>
        <table>
            <tr>
                <th class="column-1">Customer Name</th>
                <th class="column-2">Phone number</th>
                <td>Action</td>
            </tr>
            <tr v-for="a in customer">
                <td>{{ a.name }}</td>
                <td>{{ a.phone }}</td>
                <td> <button class="text-red-600 hover:underline" @click="deleteCustomer(a)">
                        Delete
                    </button></td>
            </tr>
        </table>

    </div>



</template>
