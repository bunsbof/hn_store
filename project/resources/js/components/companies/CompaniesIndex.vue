<template>
    <div
        class="overflow-hidden overflow-x-auto min-w-full align-middle sm:rounded-md"
    >
        <div class="flex place-content-end mb-4">
            <div
                class="px-4 py-2 text-white cursor-pointer inline-flex items-center bg-gray-800 border border-transparent rounded-md font-semibold text-xs uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150"
            >
                <router-link
                    :to="{ name: 'companies.create' }"
                    class="text-sm font-medium"
                    >Create Company</router-link
                >
            </div>
        </div>

        <table class="auto">
            <thead>
                <tr>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Name</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Email</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Address</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Website</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Created Time</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Updated Time</span
                        >
                    </th>
                    <th>
                        <span
                            class="text-xs font-medium tracking-wider leading-4 text-left text-gray-500 uppercase"
                            >Actions</span
                        >
                    </th>
                </tr>
            </thead>

            <tbody>
                <template v-for="item in companies" :key="item.id">
                    <tr>
                        <td>
                            {{ item.name }}
                        </td>
                        <td>
                            {{ item.email }}
                        </td>
                        <td>
                            {{ item.address }}
                        </td>
                        <td>
                            {{ item.website }}
                        </td>
                        <td>
                            {{ item.created_at }}
                        </td>
                        <td>
                            {{ item.updated_at }}
                        </td>

                        <td>
                            <router-link
                                :to="{
                                    name: 'companies.edit',
                                    params: { id: item.id },
                                }"
                                class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150"
                                >Edit</router-link
                            >
                            <button
                                class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150"
                                @click="deleteCompany(item.id)"
                            >
                                Delete
                            </button>
                        </td>
                    </tr>
                </template>
            </tbody>
        </table>
    </div>
</template>

<script>
import useCompanies from "../../composables/companies";
import { onMounted } from "vue";

export default {
    setup() {
        const { companies, getCompanies, destroyCompany } = useCompanies();

        onMounted(getCompanies);

        const deleteCompany = async (id) => {
            if (!window.confirm("Are you sure ?")) {
                return;
            }
            await destroyCompany(id);
            await getCompanies();
        };

        return {
            companies,
            deleteCompany,
        };
    },
};
</script>
