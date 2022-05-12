<script setup>
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
import {Head} from '@inertiajs/inertia-vue3';
import {onMounted, reactive, ref} from "vue";
import Paginate from "vuejs-paginate-next";

const customers = ref({
    data: [],
    to: 1,
    from: 1,
    total: 1,
    links: []
})

const fetchCustomer = (fetchUrl = null) => {
    let url = fetchUrl ? fetchUrl : '/customer'
    axios.get(url).then(response => {
        customers.value = response.data
    })
}

onMounted(() => {
    fetchCustomer()
})

</script>

<template>
    <Head title="Dashboard"/>

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Customers
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">


                        <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
                            <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                                <thead
                                    class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                                <tr>
                                    <th scope="col" class="px-6 py-3">
                                        Name
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        Description
                                    </th>
                                </tr>
                                </thead>
                                <tbody>
                                <tr v-for="customer of customers.data"
                                    class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                    <th scope="row"
                                        class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                                        {{ customer.name }}
                                    </th>
                                    <td class="px-6 py-4">
                                        {{ customer.description }}
                                    </td>
                                </tr>
                                </tbody>
                            </table>
                        </div>

                        <!-- This example requires Tailwind CSS v2.0+ -->
                        <div
                            class="bg-white px-4 py-3 flex items-center justify-between border-t border-gray-200 sm:px-6">
                            <div class="flex-1 flex justify-between sm:hidden">
                                <a href="#"
                                   class="relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50">
                                    Previous </a>
                                <a href="#"
                                   class="ml-3 relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50">
                                    Next </a>
                            </div>
                            <div class="hidden sm:flex-1 sm:flex sm:items-center sm:justify-between">
                                <div>
                                    <p class="text-sm text-gray-700">
                                        Showing
                                        <span class="font-medium">{{ customers.to }}</span>
                                        to
                                        <span class="font-medium">{{ customers.from }}</span>
                                        of
                                        <span class="font-medium">{{ customers.total }}</span>
                                        results
                                    </p>
                                </div>
                                <div>
                                    <nav class="relative z-0 inline-flex rounded-md shadow-sm -space-x-px"
                                         aria-label="Pagination">
                                        <!-- Current: "z-10 bg-indigo-50 border-indigo-500 text-indigo-600", Default: "bg-white border-gray-300 text-gray-500 hover:bg-gray-50" -->
                                        <a v-for="link in customers.links" @click="fetchCustomer(link.url)" href="#"
                                           aria-current="page"
                                           :class="link.active ? 'z-10 bg-indigo-50' : 'bg white border-gray-300'"
                                           class="border-indigo-500 text-indigo-600 relative inline-flex items-center px-4 py-2 border text-sm font-medium">
                                            {{ link.label }} </a>

                                    </nav>
                                </div>
                            </div>
                        </div>


                    </div>
                </div>
            </div>

        </div>
    </BreezeAuthenticatedLayout>
</template>
