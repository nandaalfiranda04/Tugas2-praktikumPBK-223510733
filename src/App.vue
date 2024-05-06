<template>
    <div class="container mt-3">
      <div class="card">
        <div class="text-center mt-2">
          <h2>MATA KULIAH</h2>
        </div>
        <div class="card-body">
          <div class="mt-2">
            <!-- Input form untuk menambah kegiatan baru -->
            <table class="table table-bordered mt-3">
              <thead>
                <tr>
                  <th>Mata Kuliah</th>
                  <th>Jam</th>
                  <th>Hari</th>
                  <th>Ruangan</th>
                  <th>Tindakan</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td><input type="text" v-model="newActivity.name" placeholder="Nama Mata Kuliah"></td>
                  <td><input type="time" v-model="newActivity.time" placeholder="Jam"></td>
                  <td>
                    <select v-model="newActivity.day">
                      <option value="Senin">Senin</option>
                      <option value="Selasa">Selasa</option>
                      <option value="Rabu">Rabu</option>
                      <option value="Kamis">Kamis</option>
                      <option value="Jumat">Jumat</option>
                    </select>
                  </td>
                  <td><input type="text" v-model="newActivity.room" placeholder="Ruangan"></td>
                  <td>
                    <button class="btn btn-primary" @click="addOrUpdateActivity()">
                      {{ isEditing ? 'Update' : 'Tambah' }}
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
  
          <!-- Tabel untuk menampilkan kegiatan -->
          <table class="table table-bordered mt-3">
            <thead>
              <tr>
                <th>No</th>
                <th>Nama Mata Kuliah</th>
                <th>Jam</th>
                <th>Hari</th>
                <th>Ruangan</th>
                <th>Tindakan</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(activity, index) in activities" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ activity.name }}</td>
                <td>{{ activity.time }}</td>
                <td>{{ activity.day }}</td>
                <td>{{ activity.room }}</td>
                <td>
                  <button type="button" class="btn btn-primary" @click="editActivity(activity)">Edit</button>
                  <button type="button" class="btn btn-danger" @click="removeActivity(index)">Delete</button>
                </td>
              </tr>
              <tr v-if="activities.length === 0">
                <td colspan="6">No activities</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Mata Kuliah',
    data() {
      return {
        activities: [],
        newActivity: {
          name: '',
          time: '',
          day: 'Senin',
          room: ''
        },
        isEditing: false,
        editIndex: null
      };
    },
    mounted() {
      this.getActivities();
    },
    methods: {
      getActivities() {
        // Panggil API atau lakukan pengisian dari sumber lainnya
        // Misalnya, saya menggantinya dengan data palsu untuk simulasi
        this.activities = [
          { name: 'PEMROGRAMAN BERBASIS KOMPONEN', time: '13:00', day: 'Rabu', room: 'C301' }
        ];
      },
      addOrUpdateActivity() {
        if (this.isEditing) {
          this.activities[this.editIndex] = { ...this.newActivity };
          this.isEditing = false;
          this.editIndex = null;
        } else {
          if (this.newActivity.name.trim() !== '' && this.newActivity.time.trim() !== '' && this.newActivity.room.trim() !== '') {
            this.activities.push({ ...this.newActivity });
          }
        }
        this.clearForm();
      },
      editActivity(activity) {
        this.newActivity = { ...activity };
        this.isEditing = true;
        this.editIndex = this.activities.indexOf(activity);
      },
      removeActivity(index) {
        this.activities.splice(index, 1);
      },
      clearForm() {
        this.newActivity = {
          name: '',
          time: '',
          day: 'Senin',
          room: ''
        };
      }
    }
  };
  </script>
  