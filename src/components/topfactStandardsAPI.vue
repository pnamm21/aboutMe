<template>
  <div class="container mt-5">
    <img src="https://topfact.de/files/topfact/logo/logo-neu.png" alt="Logo" style="width: 300px; height: 100px; margin-right: 10px;" />
    <h1 class="mb-4">Standards Übersicht</h1>
    
    <div class="form-group">
      <label for="xmlNameSelect">XML Name auswählen</label>
      <select v-model="selectedXmlName" class="form-control" id="xmlNameSelect">
        <option v-for="(name, index) in xmlNames" :key="index" :value="name">
          {{ name }}
        </option>
      </select>
    </div>

    <div class="mt-3">
      <button @click="resetSelection" class="btn btn-secondary mr-2">Auswahl zurücksetzen</button>
      <button @click="downloadXml" class="btn btn-primary" :disabled="!selectedXmlName">Download</button>
    </div>

    <table class="table table-striped table-hover mt-4">
      <thead class="table-dark">
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>Beschreibung</th>
          <th>Gültigkeit Ab</th>
          <th>Gültigkeit Bis</th>
          <th>Kategorie</th>
          <th>Verantwortlich</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="standard in filteredStandards" :key="standard.id">
          <td>{{ standard.id }}</td>
          <td>{{ standard.name }}</td>
          <td>{{ standard.beschreibung }}</td>
          <td>{{ formatDate(standard.gültigkeitAb) }}</td>
          <td>{{ formatDate(standard.gültigkeitBis) }}</td>
          <td>{{ standard.kategorie }}</td>
          <td>{{ standard.verantwortlich }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      standards: [],
      xmlNames: [], // Liste der XML-Namen
      selectedXmlName: "", // Der aktuell ausgewählte XML-Name
    };
  },
  mounted() {
    this.fetchXmlNames();
    this.fetchStandards();
  },
  methods: {
    async fetchXmlNames() {
      try {
        const response = await fetch('https://localhost:44337/api/StandardsXML/names');
        const data = await response.json();
        this.xmlNames = data;
      } catch (error) {
        console.error('Fehler beim Abrufen der XML-Namen:', error);
      }
    },
    async fetchStandards() {
      try {
        const response = await fetch('https://localhost:44337/api/Standard');
        const data = await response.json();
        this.standards = data;
      } catch (error) {
        console.error('Fehler beim Abrufen der Standards-Daten:', error);
      }
    },
    formatDate(date) {
      if (!date) return 'N/A';
      const d = new Date(date);
      return d.toISOString().split('T')[0];
    },
    resetSelection() {
      // Setzt die Auswahl auf null zurück
      this.selectedXmlName = "";
    },
    async downloadXml() {
  if (!this.selectedXmlName) return;

  try {
    const response = await fetch(`https://localhost:44337/api/StandardsXML/${this.selectedXmlName}`);
    if (!response.ok) {
      throw new Error('XML-Datei konnte nicht heruntergeladen werden');
    }

    const blob = await response.blob();
    console.log(blob);  // Überprüfen Sie den Blob-Inhalt in der Konsole
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = `${this.selectedXmlName}.xml`;
    link.click();
  } catch (error) {
    console.error('Fehler beim Herunterladen der Datei:', error);
  }
}

  },
  computed: {
    filteredStandards() {
      if (!this.selectedXmlName) return this.standards;
      return this.standards.filter(standard => standard.name === this.selectedXmlName);
    }
  }
};
</script>

<style scoped>
.table {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
}

.table th,
.table td {
  text-align: center;
  padding: 8px;
}

.table th {
  background-color: #343a40;
  color: white;
}

.table-striped tbody tr:nth-child(odd) {
  background-color: #f2f2f2;
}

.table-hover tbody tr:hover {
  background-color: #dcdcdc;
}

.table td {
  border-bottom: 1px solid #ddd;
}
</style>
