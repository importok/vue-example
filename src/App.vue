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
            // Simulate a network request for 100ms
            await new Promise(resolve => setTimeout(resolve, 200));

            if (record.rowIndex % 5 === 0) {
              // Simulate a failure for every 5th record
              record.markAsRejected();
            }
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
                    validators: 'required',
                    transformers: 'capitalize|trim'
                },
                email: {
                    label: 'Email',
                    validators: 'email|required',
                    transformers: 'lowercase|trim'
                },
                phone: {
                    label: 'Phone',
                    transformers: 'trim'
                },
                country: {
                    label: 'Country',
                    transformers: 'trim|as:countries',
                    validators: 'in:countries',
                    provider: 'countries'
                },
            },
        };
    }
};
</script>
<template>
    <div style="margin: 2rem;">
        <ImportokWizard
            title="ImportOK Example for Vue"
            :fields="fields"
            sample-file="/sample.csv"
            @record-ready="saveRecord"
        />
    </div>
</template>