<template>
  <div class="">
    Current Edit Mode: <strong>{{ editMode }}</strong>
    <DataTable
      :value="tableContents"
      :editMode="editMode"
      @cell-edit-complete="onCellEditComplete"
      class="editable-cells-table"
      responsiveLayout="scroll"
    >
      <Column
        v-for="col of columns"
        :field="col.field"
        :header="col.header"
        :key="col.field"
        style="width: 25%"
      >
        <template #body="{ data, field }">
          <slot :name="col.field">
            <small>{{ data[field] }}</small>
          </slot>
        </template>

        <template #editor="slotProps">
          <slot :name="`${col.field}edit`">
            <InputText
              v-model="slotProps.data[slotProps.column.field]"
              autofocus
            />
            <button @click="OnEditComplete(slotProps)">EXIT</button>
          </slot>
        </template>
      </Column>
    </DataTable>
  </div>
</template>




<script>
// import RhTable from "@/components/RhTable/RhTable.vue";
// import RhCard from "./components/RhCard/RhCard.vue";
// import RhChip from "./components/RhChip/RhChip.vue";
// import RhSelect from "./components/RhSelect/RhSelect.vue";
// import RhSearchBar from "./components/RhSearchBar/RhSearchBar.vue";
// import RhTextField from "./components/RhTextField/RhTextField.vue";

import Column from "primevue/column";
import DataTable from "primevue/datatable";
import InputText from "primevue/inputtext";
export default {
  components: {
    // RhDashboardLayout,
    InputText,
    // RhCard,
    // RhTable,
    // RhChip,
    // RhTextField,
    Column,
    // RhSelect,
    DataTable,
    // RhSearchBar,
  },
  data() {
    return {
      value: "1",
      editMode: "cell",
      myValue: "1234",
      tableContents: [
        {
          name: "aaaaaaa",
          project_name: "bbbb",
          id: "1",
          default: 11,
          village: "charwan",
        },
        {
          name: "ccccc",
          project_name: "ddddd",
          id: "2",
          default: 22,
          village: "oo",
        },
        {
          name: "eeee",
          project_name: "fffffff",
          id: "3",
          default: 33,
          village: "opppp",
        },
      ],
      isApart: true,
      columns: [
        {
          field: "name",
          header: "NAME",
          sortable: true,
          cellWidth: "30%",
        },
        {
          field: "project_name",
          header: "PROJECT",
          sortable: true,
          cellWidth: "40%",
        },
        // {
        //   field: "status",
        //   header: "Status",
        //   type: "select",
        //   items: ["Available", "Not available", "Sold out"],
        // },

        {
          field: "id",
          header: "IDD",
          // type: "action",
          // icon: "pencil",
          cellWidth: "8%",

          // function: this.openLPBuilder,
        },
      ],
    };
  },
  methods: {
    // auto edit complete
    onCellEditComplete(ee) {
      let { data, newValue, field } = ee;

      console.log(data, newValue, field, "KKKKKKK");
      console.log("ON CELL EDIT COMPLETE", ee.type);

      // ee.stop

      // ee.preventDefault();
      // data[field] = "AAAAAAAa";
    },

    // custom edit click ( from text field)

    OnEditComplete(event) {
      let { data, newValue, field } = event;

      console.log(data, newValue, field);

      console.log("OK CHECK MARK CICKED", event);
      data[field] = "something new";
      // this.editMode = "row";
    },
  },
};
</script>
