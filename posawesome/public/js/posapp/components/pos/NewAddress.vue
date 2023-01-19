<template>
  <v-row justify="center">
    <v-dialog v-model="addressDialog" max-width="600px">
      <v-card>
        <v-card-title>
          <span class="headline primary--text">{{
          __('Add New Address')
          }}</span>
        </v-card-title>
        <div id="tab-app" class="container">
          <ul class="tabs-choose">
            <li @click="activeTab='1'" :class="[activeTab === '1' ? 'active' : '']">Address</li>
            <!-- <li @click="activeTab='2'" :class="[activeTab === '2' ? 'active' : '']">Adress Detail</li> -->
            <!-- <li @click="activeTab='3'" :class="[activeTab === '3' ? 'active' : '']">Other</li> -->
          </ul>
          <div class="tabs-content">
            <div class="content-one" v-if="activeTab === '1'">
              <v-row>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('City')"
                  v-model="city" :items="cities" background-color="white" :no-data-text="__('Cities not found')"
                  hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Sub District')"
                  v-model="subdistrict" :items="subdistricts" background-color="white"
                  :no-data-text="__('Sub District not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('District')"
                  v-model="district" :items="districts" background-color="white"
                  :no-data-text="__('District not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Branch')"
                  v-model="branch" :items="branches" background-color="white"
                  :no-data-text="__('Branch Charge not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Delivery Charge')"
                  v-model="dcharge" :items="dcharges" background-color="white"
                  :no-data-text="__('Delivery Charge not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-text-field label="Time To Deliver" dense color="primary" background-color="white" hide-details
                  v-model="TimeToDeliver"></v-text-field>
              </v-col>
            </v-row>
              <v-row>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Address Name')" background-color="white"
                    hide-details v-model="address.name"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Address Line 1')" background-color="white"
                    hide-details v-model="address.address_line1"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Phone')" background-color="white"
                    hide-details v-model="address.phone"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Street')" background-color="white"
                    hide-details v-model="address.street"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Building')" background-color="white"
                    hide-details v-model="address.building"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Floor')" background-color="white"
                    hide-details v-model="address.floor"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Flat')" background-color="white"
                    hide-details v-model="address.flat"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Landmark')" background-color="white"
                    hide-details v-model="address.landmark"></v-text-field>
                </v-col> 
              </v-row>  
  
            </div>
            <div class="content-one" v-if="activeTab === '2'">
              <v-row>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Address Name')" background-color="white"
                    hide-details v-model="address.name"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Address Line 1')" background-color="white"
                    hide-details v-model="address.address_line1"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Phone')" background-color="white"
                    hide-details v-model="address.phone"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Street')" background-color="white"
                    hide-details v-model="address.street"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Building')" background-color="white"
                    hide-details v-model="address.building"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Floor')" background-color="white"
                    hide-details v-model="address.floor"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Flat')" background-color="white"
                    hide-details v-model="address.flat"></v-text-field>
                </v-col>
                <v-col cols="6">
                  <v-text-field dense color="info" :label="frappe._('Landmark')" background-color="white"
                    hide-details v-model="address.landmark"></v-text-field>
                </v-col>
                
              </v-row>
            </div>

            <!-- <div class="content-one" v-if="activeTab === '3'">Content Three</div> -->
          </div>
        </div>
        <!-- <v-card-text class="pa-0">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field dense color="primary" :label="frappe._('Address Name')" background-color="white"
                  hide-details v-model="address.name"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field dense color="primary" :label="frappe._('Address Line 1')" background-color="white"
                  hide-details v-model="address.address_line1"></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('City')"
                  v-model="city" :items="cities" background-color="white" :no-data-text="__('Cities not found')"
                  hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('District')"
                  v-model="district" :items="districts" background-color="white"
                  :no-data-text="__('District not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Sub District')"
                  v-model="subdistrict" :items="subdistricts" background-color="white"
                  :no-data-text="__('Sub District not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Delivery Charge')"
                  v-model="dcharge" :items="dcharges" background-color="white"
                  :no-data-text="__('Delivery Charge not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-autocomplete clearable dense auto-select-first color="primary" :label="frappe._('Branch')"
                  v-model="branch" :items="branches" background-color="white"
                  :no-data-text="__('Branch Charge not found')" hide-details>
                </v-autocomplete>
              </v-col>
              <v-col cols="6">
                <v-text-field label="Time To Deliver" dense color="primary" background-color="white" hide-details
                  v-model="TimeToDeliver"></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text> -->
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="info" dark @click="getdc">{{
          __('Get Charge')
          }}</v-btn>
          <v-btn color="success" dark @click="submit_dialog">{{
          __('Submit')
          }}</v-btn>
          <v-btn color="error" dark @click="close_dialog">{{
          __('Close')
          }}</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import { evntBus } from '../../bus';
export default {
  data: () => ({
    addressDialog: false,
    activeTab: '1',
    address: {},
    subdistrict: '',
    subdistricts: [],
    customer: '',
    city: 'Cairo',
    cities: [],
    dcharge: '',
    dcharges: [],
    district: '',
    districts: [],
    branch: '',
    branches: [],
    TimeToDeliver: '90',
    dc: [],
  }),
  methods: {
    close_dialog() {
      this.addressDialog = false;
    },

    getsubdistrict() {
      if (this.subdistricts.length > 0) return;
      const vm = this;
      frappe.db
        .get_list('Sub District', {
          fields: ['name', 'territory', 'branch', 'delivery_charges'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              vm.subdistricts.push(el.name);
              vm.dc.push(el.delivery_charges);
              vm.dc.forEach((dce) => {
                if (dce == this.subdistrict) {
                  console.log('fine')
                }
              }
              )
            });
          }
        });
    },
    getcities() {
      if (this.cities.length > 0) return;
      const vm = this;
      frappe.db
        .get_list('Cities', {
          fields: ['name', 'country'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              vm.cities.push(el.name);
            });
          }
        });
    },
    getdc() {
      const vm = this;
      this.dcharges = [];
      this.districts = [];
      this.branches = [];
      frappe.db
        .get_list('Sub District', {
          fields: ['name', 'territory', 'branch', 'delivery_charges'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              console.log(el.territory)
              console.log(vm.districts)
              vm.dc.forEach((dce) => {
                if (el.delivery_charges == dce && el.name == this.subdistrict) {
                  vm.dcharges.push(dce)
                  vm.districts.push(el.territory)
                  vm.branches.push(el.branch)
                }
              }
              )
            });
            vm.branches = vm.branches
            console.log('branch', this.branch)
          }
        });
    },
    submit_dialog() {
      const vm = this;
      this.address.customer = this.customer;
      this.address.doctype = 'Customer';
      this.address.subdistrict = this.subdistrict;
      this.address.city = this.city;
      this.address.dcharge = this.dcharge
      this.address.branch = this.branch
      console.log(this.address)
      frappe.call({
        method: 'posawesome.posawesome.api.posapp.make_address',
        args: {
          args: this.address,
        },
        callback: (r) => {
          if (!r.exc) {
            evntBus.$emit('add_the_new_address', r.message);
            evntBus.$emit('show_mesage', {
              text: 'Customer Address created successfully.',
              color: 'success',
            });
            vm.customer = '';
            vm.address = {};
            vm.subdistrict = '';
            vm.city = '';
            vm.dcharge = '';
            vm.addressDialog = false;
          }
        },
      });
    },
  },
  created: function () {
    evntBus.$on('open_new_address', (data) => {
      this.addressDialog = true;
      this.customer = data;
    });
    this.getsubdistrict();
    this.getcities();
  },
};
</script>

<style scoped src="../../../main.css">

</style>
