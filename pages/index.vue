<template>
  <div class="dashboard">
    <v-container class="my-5">
      <h1 class="text-center subheading grey--text my-10">
        myTCA
      </h1>

      <v-row justify="center" class="mx-3">
        <v-col cols="12" sm="6" md="4">
          <v-text-field
            prepend-inner-icon="mdi-magnify"
            placeholder="Search ic or name"
            outlined
            rounded
            dense
            clearable
          />
        </v-col>
      </v-row>

      <v-row justify="start" class="mb-3">
        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn small text color="grey" @click="sortBy('title')" v-on="on">
              <v-icon small left>
                mdi-folder
              </v-icon>
              <span class="caption text-lowercase">By Project Name</span>
            </v-btn>
          </template>
          <span>Sort by project name</span>
        </v-tooltip>

        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn small text color="grey" @click="sortBy('person')" v-on="on">
              <v-icon small left>
                mdi-account
              </v-icon>
              <span class="caption text-lowercase">By Person</span>
            </v-btn>
          </template>
          <span>Sort by project author</span>
        </v-tooltip>
      </v-row>

      <v-expansion-panels>
        <v-expansion-panel :key="patient1">
          <v-expansion-panel-header class="py-1">
            Patient1
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-card v-for="project in projects" :key="project.title" flat>
              <v-row wrap :class="`pa-3 project ${project.status}`">
                <v-col xs="12" md="6">
                  <div class="caption grey--text">
                    Project title
                  </div>
                  <div>{{ project.title }}</div>
                </v-col>
                <v-col xs="6" sm="4" md="2">
                  <div class="caption grey--text">
                    Person
                  </div>
                  <div>{{ project.person }}</div>
                </v-col>
                <v-col xs="6" sm="4" md="2">
                  <div class="caption grey--text">
                    Due by
                  </div>
                  <div>{{ project.due }}</div>
                </v-col>
                <v-col xs="2" sm="4" md="2">
                  <div class="right">
                    <v-chip small :class="`${project.status} white--text my-2 caption`">
                      {{ project.status }}
                    </v-chip>
                  </div>
                </v-col>
              </v-row>
              <v-divider />
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-container>
  </div>
</template>

<script>
export default {
  data () {
    return {
      projects: [
        { title: 'Design a new website', person: 'The Net Ninja', due: '1st Jan 2019', status: 'ongoing', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!' },
        { title: 'Code up the homepage', person: 'Chun Li', due: '10th Jan 2019', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!' },
        { title: 'Design video thumbnails', person: 'Ryu', due: '20th Dec 2018', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!' },
        { title: 'Create a community forum', person: 'Gouken', due: '20th Oct 2018', status: 'overdue', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!' }
      ]
    }
  },
  methods: {
    sortBy (prop) {
      this.projects.sort((a, b) => a[prop] < b[prop] ? -1 : 1)
    }
  }
}
</script>

<style>

.project.complete{
  border-left: 4px solid #3cd1c2;
}
.project.ongoing{
  border-left: 4px solid #ffaa2c;
}
.project.overdue{
  border-left: 4px solid #f83e70;
}
.v-chip.v-chip--no-color.complete{
  background: #3cd1c2;
}
.v-chip.v-chip--no-color.ongoing{
  background: #ffaa2c;
}
.v-chip.v-chip--no-color.overdue{
  background: #f83e70;
}

</style>
