<template>
  <div>
    <h1 class="mb-8 text-3xl font-bold">
      <Link class="text-indigo-400 hover:text-indigo-600" href="/contacts">Contacts</Link>
      <span class="text-indigo-400 font-medium">/</span> Create
    </h1>
    <div class="max-w-3xl bg-white rounded-md shadow overflow-hidden">
      <form @submit.prevent="store">
        <div class="flex flex-wrap -mb-8 -mr-6 p-8">
          <text-input v-model="form.first_name" :error="form.errors.first_name" class="pb-8 pr-6 w-full lg:w-1/2" label="First name" />
          <text-input v-model="form.last_name" :error="form.errors.last_name" class="pb-8 pr-6 w-full lg:w-1/2" label="Last name" />
          <select-input v-model="form.organization_id" :error="form.errors.organization_id" class="pb-8 pr-6 w-full lg:w-1/2" label="Organization">
            <option value=""></option>
            <option v-for="organization in organizations" :key="organization.id" :value="organization.id">{{ organization.name }}</option>
          </select-input>
          <text-input v-model="form.email" :error="form.errors.email" class="pb-8 pr-6 w-full lg:w-1/2" label="Email" />
          <text-input v-model="form.phone" :error="form.errors.phone" class="pb-8 pr-6 w-full lg:w-1/2" label="Phone" />
          <text-input v-model="form.address" :error="form.errors.address" class="pb-8 pr-6 w-full lg:w-1/2" label="Address" />
          <text-input v-model="form.city" :error="form.errors.city" class="pb-8 pr-6 w-full lg:w-1/2" label="City" />
          <text-input v-model="form.region" :error="form.errors.region" class="pb-8 pr-6 w-full lg:w-1/2" label="Province/State" />
          <select-input v-model="form.country" :error="form.errors.country" class="pb-8 pr-6 w-full lg:w-1/2" label="Country">
            <option value=""></option>
            <option value="CA">Canada</option>
            <option value="US">United States</option>
          </select-input>
          <text-input v-model="form.postal_code" :error="form.errors.postal_code" class="pb-8 pr-6 w-full lg:w-1/2" label="Postal code" />
        </div>
        <div class="flex items-center justify-end px-8 py-4 bg-gray-50 border-t border-gray-100">
          <loading-button :loading="form.processing" class="btn-indigo" type="submit">Create Contact</loading-button>
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import { Link, useForm } from '@inertiajs/inertia-vue3'
import { Organization } from '@/models'
import Layout from '@/common/Layout.vue'
import TextInput from '@/common/TextInput.vue'
import SelectInput from '@/common/SelectInput.vue'
import LoadingButton from '@/common/LoadingButton.vue'

export default defineComponent({
  components: {
    Link,
    LoadingButton,
    SelectInput,
    TextInput,
  },
  layout: Layout,
  props: {
    organizations: {
      type: Array as PropType<Organization[]>,
      required: true
    }
  },
  data() {
    return {
      form: useForm({
        first_name: '',
        last_name: '',
        organization_id: '',
        email: '',
        phone: '',
        address: '',
        city: '',
        region: '',
        country: '',
        postal_code: '',
      }),
    }
  },
  methods: {
    store() {
      const route = this.$route("contacts.create")
      this.form.post(route)
    },
  },
})
</script>
