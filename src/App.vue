<script>
import ImportokWizard from "@importok/vue";

export default {
    components: {
        ImportokWizard
    },

    methods: {
        /**
         * Push the provided record to the API
         * Check https://importok.io/docs/webhooks.html for more details
         */
        async saveRecord(record, meta) {
            console.log('Record:', record);
            console.log('Meta:', meta);
            return await fetch('https://httpstat.us/200');
        }
    },

    data() {
        return {
            /**
             * Import fields to be mapped
             * Check https://importok.io/docs/fields.html for more details
             */
            fields: {
                first_name: {
                    label: 'First Name',
                    transformers: 'capitalize|trim'
                },
                last_name: {
                    label: 'Last Name',
                    validators: 'required|length:5',
                    transformers: 'capitalize|trim'
                },
                company_name: {
                    label: 'Company Name',
                    transformers: 'trim'
                },
                email: {
                    label: 'Email',
                    validators: 'email|required',
                    transformers: 'lowercase|trim'
                },
            }
        };
    }
};
</script>
<template>
    <ImportokWizard
        title="ImportOK Example for Vue"
        :fields="fields"
        sample-file="/sample.csv"
        @record-ready="saveRecord"
    />
</template>