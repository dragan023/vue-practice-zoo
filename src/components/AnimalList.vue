<template>
  <div class="c-container">
    <div class="c-container__column">
      <form @submit.prevent="handleSubmit">
        <h3>Add Animal</h3>
        <div class="c-form-row">
          <label for="name">Name</label>
          <input v-model="animalToAdd.name" type="text" name="name" id="name" />
        </div>

        <div class="c-form-row">
          <label for="type">Type</label>
          <input v-model="animalToAdd.type" type="text" name="type" id="type" />
        </div>

        <div class="c-form-row">
          <label for="date">Date of birth</label>
          <input type="date" :value="animalToAdd.dateOfBirth" />
        </div>

        <select v-model="animalToAdd.type">
          <option disabled value="">Please select one</option>
          <option v-for="type in types" :key="type">{{ type }}</option>
        </select>

        <button type="submit">add</button>
      </form>

      <div class="c-list-wrapper">
        <h1>Types</h1>
        <ul>
          <li v-for="type in types" :key="type">
            <p>{{ type }}</p>
            <button @click="alertTypes(type)">
              see animal list of those type
            </button>
          </li>
        </ul>
      </div>
    </div>
    <div class="c-container__column">
      <div class="c-list-wrapper">
        <h1>Animals</h1>

        <div class="l-animal-grid">
          <div
            class="l-animal-grid__item"
            v-for="animal in animals"
            :key="animal.id"
          >
            <div class="c-animal-card">
              <p>{{ animal.type }}</p>
              <p>{{ animal.name }}</p>
              <p>
                {{
                  animal.dateOfBirth
                    ? animal.dateOfBirth.toLocaleDateString()
                    : 'unknown'
                }}
              </p>
              <button @click="removeAnimal(animal.id)">remove</button>
              <button @click="moveToTop(animal.id)">move to top</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      animals: [
        {
          id: 0,
          type: 'fish',
          name: 'neko ime',
          dateOfBirth: new Date(1995, 12, 17)
        },
        {
          id: 1,
          type: 'bird',
          name: 'neko ime',
          dateOfBirth: new Date(1995, 12, 17)
        },
        {
          id: 2,
          type: 'reptile',
          name: 'neko ime',
          dateOfBirth: new Date(1995, 12, 17)
        },
        {
          id: 3,
          type: 'mammals',
          name: 'neko ime',
          dateOfBirth: ''
        },
        {
          id: 4,
          type: 'Amphibians',
          name: 'neko ime',
          dateOfBirth: new Date(1995, 12, 17)
        },
        {
          id: 5,
          type: 'fish',
          name: 'neko ime',
          dateOfBirth: new Date(1995, 12, 17)
        }
      ],
      types: ['Fish', 'Bird', 'Reptile', 'Mammals', 'Amphibians'],
      movedAnimal: {},
      animalToAdd: {
        dateOfBirth: new Date(),
        name: '',
        type: ''
      }
    };
  },
  methods: {
    removeAnimal(id) {
      this.animals = this.animals.filter(animal => animal.id !== id);
    },

    moveToTop(id) {
      this.animals.forEach((animal, index) => {
        if (animal.id !== id) {
          return false;
        }

        this.movedAnimal = this.animals[index];
        this.animals.splice(index, 1);
        this.animals.unshift(this.movedAnimal);
      });
    },
    handleSubmit() {
      this.animals.push(this.animalToAdd);
    },
    alertTypes(type) {
      alert(
        JSON.stringify(
          this.animals.filter(
            animal => animal.type.toLowerCase() === type.toLowerCase()
          )
        )
      );
    }
  }
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.l-animal-grid {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -15px;
}

.l-animal-grid__item {
  flex-basis: calc(100% / 3);
  padding: 0 15px;
}
.c-container__column {
  display: flex;
  justify-content: flex-end;
  padding: 20px;
}

.c-container__column:first-child {
  flex-direction: column;
}

.c-container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

ul {
  list-style: none;
  padding: 0;
}

.c-form-row {
  display: flex;
}

input {
  flex-grow: 1;
  padding: 10px 20px;
  border-radius: 4px;
  background-image: none;
  border: 1px solid #bbb;
  box-shadow: none;
  appearance: none;
}

label {
  width: 100px;
}

h1 {
  margin-bottom: 5px;
}

.c-animal-card {
  background: rgb(133, 152, 170);
  padding: 10px 20px;
  border-bottom: 1px solid #123;
  border-radius: 4px;
  margin-bottom: 10px;
}
</style>
