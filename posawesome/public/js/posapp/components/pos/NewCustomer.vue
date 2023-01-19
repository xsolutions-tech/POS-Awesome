<template>
  <v-row justify="center">
    <v-dialog v-model="customerDialog" max-width="600px">
      <v-card>
        <v-card-title>
          <span class="headline primary--text">{{ __('New Customer') }}</span>
        </v-card-title>
        <v-card-text class="pa-0">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  dense
                  color="primary"
                  :label="frappe._('Customer Name')"
                  background-color="white"
                  hide-details
                  v-model="customer_name"
                ></v-text-field>
              </v-col>
              <!-- <v-col cols="6">
                <v-autocomplete
                  clearable
                  dense
                  auto-select-first
                  color="primary"
                  :label="frappe._('Sub District')"
                  v-model="sd"
                  :items="sds"
                  background-color="white"
                  :no-data-text="__('Sub District not found')"
                  hide-details
                >
                </v-autocomplete>
              </v-col>
              
              <v-col cols="6">
                <v-text-field
                  dense
                  color="primary"
                  :label="frappe._('Tax ID')"
                  background-color="white"
                  hide-details
                  v-model="tax_id"
                ></v-text-field>
              </v-col> -->
              <v-col cols="6">
                <v-text-field
                  dense
                  color="primary"
                  :label="frappe._('Mobile No')"
                  background-color="white"
                  hide-details
                  v-model="mobile_no"
                ></v-text-field>
              </v-col>
              <!-- <v-col cols="6">
                <v-text-field
                  dense
                  color="primary"
                  :label="frappe._('Email Id')"
                  background-color="white"
                  hide-details
                  v-model="email_id"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  dense
                  color="primary"
                  :label="frappe._('Referral Code')"
                  background-color="white"
                  hide-details
                  v-model="referral_code"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-menu
                  ref="birthday_menu"
                  v-model="birthday_menu"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  dense
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="birthday"
                      :label="frappe._('Birthday')"
                      readonly
                      dense
                      clearable
                      hide-details
                      v-bind="attrs"
                      v-on="on"
                      color="primary"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="birthday"
                    color="primary"
                    no-title
                    scrollable
                    :max="frappe.datetime.now_date()"
                    @input="birthday_menu = false"
                  >
                  </v-date-picker>
                </v-menu>
              </v-col> -->
              <v-col cols="6">
                <v-autocomplete
                  clearable
                  dense
                  auto-select-first
                  color="primary"
                  :label="frappe._('District')"
                  v-model="territory"
                  :items="territorys"
                  background-color="white"
                  :no-data-text="__('District not found')"
                  hide-details
                >
                </v-autocomplete>
              </v-col> 
              <v-col cols="6">
                <v-autocomplete
                  clearable
                  dense
                  auto-select-first
                  color="primary"
                  :label="frappe._('Customer Group')"
                  v-model="group"
                  :items="groups"
                  background-color="white"
                  :no-data-text="__('Group not found')"
                  hide-details
                >
                </v-autocomplete>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <!-- <v-btn color="info" dark @click="tCheck">{{
            __('Get District')
          }}</v-btn> -->
          <!-- <v-btn color="error" dark @click="clear">{{
            __('Clear')
          }}</v-btn> -->
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
import { constants } from 'crypto';
import { evntBus } from '../../bus';
export default {
  data: () => ({
    customerDialog: false,
    pos_profile: '',
    customer_name: '',
    tax_id: '',
    sd:'',
    sds:[],
    district:[],
    mobile_no: '',
    email_id: '',
    referral_code: '',
    birthday: null,
    birthday_menu: false,
    group: '',
    groups: [],
    territory: '',
    territorys: [],
  }),
  watch: {},
  methods: {
    close_dialog() {
      this.customerDialog = false;
    },
    getCustomerGroups() {
      if (this.groups.length > 0) return;
      const vm = this;
      frappe.db
        .get_list('Customer Group', {
          fields: ['name'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              vm.groups.push(el.name);
            });
          }
        });
    },
    getsds() {
      if (this.sds.length > 0) return;
      const vm = this;
      const districts = this.district
      console.log('Dict',districts)
      frappe.db
        .get_list('Sub District', {
          fields: ['name','territory'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              vm.sds.push(el.name);
            });
          }
        });
    
    },
    tCheck(){
      const vm = this;
      vm.territorys = [];
      const terrs = this.district
      frappe.db
        .get_list('Sub District', {
          fields: ['name','territory'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              terrs.forEach((terr) => {
              if (this.sd == el.name && terr == el.territory){
              console.log(terr);
              vm.territorys.push(terr);
            }
            })
            });
          }
        });
      // console.log(terrs)
      // console.log('Global', this.sd)
    },
    getCustomerTerritorys() {
      if (this.district.length > 0) return;
      const vm = this;
      frappe.db
        .get_list('Territory', {
          fields: ['name'],
          page_length: 1000,
        })
        .then((data) => {
          if (data.length > 0) {
            data.forEach((el) => {
              vm.territorys.push(el.name);
            });
          }
          console.log(vm.district)
        });  
    },
    clear :function () {
      this.territorys = [];
    },
    submit_dialog() {
      if (this.customer_name) {
        const vm = this;
        const args = {
          customer_name: this.customer_name,
          company: this.pos_profile.company,
          tax_id: this.tax_id,
          mobile_no: this.mobile_no,
          email_id: this.email_id,
          referral_code: this.referral_code,
          birthday: this.birthday,
          customer_group: this.group,
          territory: this.territory,
        };
        frappe.call({
          method: 'posawesome.posawesome.api.posapp.create_customer',
          args: args,
          callback: (r) => {
            if (!r.exc && r.message.name) {
              evntBus.$emit('show_mesage', {
                text: __('Customer contact created successfully.'),
                color: 'success',
              });
              args.name = r.message.name;
              frappe.utils.play_sound('submit');
              evntBus.$emit('add_customer_to_list', args);
              evntBus.$emit('set_customer', r.message.name);
              vm.customer_name = '';
              vm.tax_id = '';
              vm.mobile_no = '';
              vm.email_id = '';
              vm.referral_code = '';
              vm.birthday = '';
              vm.group = '';
              vm.customerDialog = false;
            }
          },
        });
        this.customerDialog = false;
        evntBus.$emit('open_new_address', this.customer_name);
      }
    },
  },
  created: function () {
    evntBus.$on('open_new_customer', () => {
      this.customerDialog = true;
    });
    evntBus.$on('register_pos_profile', (data) => {
      this.pos_profile = data.pos_profile;
    });
    this.getCustomerGroups();
    this.getCustomerTerritorys();
    this.getsds();
  },
};
</script>
