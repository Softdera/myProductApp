<template>
  <div class="home">
    <h1>Products Available</h1>


    <!--To serach for Products by name-->
    <input type="text"
    class="searchQuery"
     v-model="searchQuery"
    placeholder="Search by Product Name">

    <!-- Search suggestions -->
    <ul v-if="searchSuggestions.length > 0" class="search-suggestions">
      <li v-for="(suggestion, index) in searchSuggestions" :key="index" @click="selectSuggestion(suggestion)">
        {{ suggestion.name }}
      </li>
    </ul>

    <!-- Sort buttons -->
    <div class="sortButtons">
    <button class="ascButton"
     @click="sortProductsByPriceInAscendingOrder">
     From Lowest Price</button>
    <button class="desButton" 
    @click="sortProductsByPriceInDescendingOrder">
    From Highest Price</button>
    
    </div>
    <!--searched Product-->
    <div class="container mt-2 pt-4" v-if="selectedProduct">
            <div class="row">
              <div class="col-md-6">
                  <div class="card my-3 list-group-item-success shadow-lg">
                    <div class="row align-items-center">
                      
                    <div class="col-md-12">
                      <ul class="list-group ">
                        <li class="list-group-item">
                          Name: <span id="fw-bold name"
                         > 
                          {{ selectedProduct.name }} </span>
                        </li>
                        <li class="list-group-item">
                          Description: <span id="fw-bold description" > {{ selectedProduct.description  }} </span>
                        </li>
                        <li class="list-group-item">
                          Price: <span id="fw-bold Price"> ${{ selectedProduct.price }} </span>
                        </li>
                        <li class="list-group-item">
                          Quantity Available: <span id="fw-bold Quantity"> {{ selectedProduct.quantity }} </span>
                        </li>
                       
                      </ul>
                    </div>
                </div>
                </div>
                </div>
                </div>
                </div>

    <!-- Pagination controls -->
    <div class="PageButtonDiv"> 
      <button class="PageButton"
      @click="prevPage" :disabled="currentPage === 1">Previous</button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button class="PageButton"
       @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
  

    <!--current Page-->
    <div class="container mt-2 pt-4" v-if="products.length > 0">
            <div class="row">
              <div class="col-md-6"  v-for="(product, index) in displayedProducts" :key="index">
                  <div class="card my-3 list-group-item-success shadow-lg">
                    <div class="row align-items-center">
                      
                    <div class="col-md-12">
                      <ul class="list-group ">
                        <li class="list-group-item">
                          Name: <span id="fw-bold name"
                         > 
                          {{ product.name }} </span>
                        </li>
                        <li class="list-group-item">
                          Description: <span id="fw-bold description" > {{ product.description  }} </span>
                        </li>
                        <li class="list-group-item">
                          Price: <span id="fw-bold Price"> ${{ product.price }} </span>
                        </li>
                        <li class="list-group-item">
                          Quantity Available: <span id="fw-bold Price"> {{ product.quantity }} </span>
                        </li>
                       
                      </ul>
                    </div>
                </div>
                </div>
                </div>
                </div>
                </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
    //HelloWorld
  },
  data (){
    return{
      products: [
        {
          id: 1,
          name: "MacBook",
          description: 'An Apple Laptop for everyday use',
          price: 14.99,
          quantity: 50
      },
      {
            name: 'Widget',
            description: 'A handy widget for various tasks',
            price: 10.99,
            quantity: 50,
            id: 2,

          },
          {
            name: 'Gadget',
            description: 'A cool gadget for everyday use',
            price: 19.99,
            quantity: 30,
            id: 3,

          },
          {
            name: 'Thingamabob',
            description: 'A mysterious thingamabob with many uses',
            price: 15.49,
            quantity: 20,
            id: 4,
          },
          {
          id: 5,
          name: "Hp Laptop",
          description: 'the laptop brand with a touch of class',
          price: 12.99,
          quantity: 55
      },
      {
            name: 'Smart Television',
            description: 'a Tv with modern features for your leisure',
            price: 10.99,
            quantity: 34,
            id: 6,

          },
          {
            name: 'Benz Cars',
            description: 'A car among cars',
            price: 59.99,
            quantity: 38,
            id: 7,

          },
          {
            name: 'Tin Milk',
            description: 'For healthy kids',
            price: 7.49,
            quantity: 23,
            id: 8,

          },
          {
          id: 9,
          name: "Coco Milo",
          description: 'A milo with a different taste',
          price: 8.99,
          quantity: 25
      },
      {
            name: 'Nokia phone',
            description: 'super phone',
            price: 13.99,
            quantity: 48,
            id: 10,

          },
          {
            name: 'iPhone XS',
            description: 'Apple products',
            price: 20.99,
            quantity: 37,
            id: 11,

          },
          {
            name: 'Eva Bottle Water',
            description: 'clean water is a necessity',
            price: 12.49,
            quantity: 29,
            id: 12,
          },
          {
          id: 13,
          name: "Water Dispenser",
          description: 'water dispenser for cold and hot water alike',
          price: 12.99,
          quantity: 55
      },
      {
            name: 'Microwave',
            description: 'heat your meals with ease',
            price: 12.99,
            quantity: 39,
            id: 14,

          },
          {
            name: 'Winco Bed',
            description: 'sleep with comfort',
            price: 49.99,
            quantity: 35,
            id: 15,

          },
          {
            name: 'Nesco Bed',
            description: 'sleep like a baby',
            price: 45.49,
            quantity: 60,
            id: 16,

          },
          {
          id: 17,
          name: "MacBook 2024",
          description: 'Latest MacBook in stores',
          price: 60.99,
          quantity: 100
      },
      {
            name: 'Pen',
            description: 'write down your brillant ideas',
            price: 5.99,
            quantity: 250,
            id: 18,

          },
          {
            name: 'Winco Chairs',
            description: 'rest easy',
            price: 25.99,
            quantity: 86,
            id: 19,

          },
          {
            name: 'plastic chairs',
            description: 'durable chairs for lasting experience',
            price: 25.49,
            quantity: 20,
            id: 20,
          },
          {
          id: 21,
          name: "Dell Laptop",
          description: 'A whole differnet experience',
          price: 14.99,
          quantity: 65
      },
      {
            name: 'Bike',
            description: 'smooth bike',
            price: 18.99,
            quantity: 78,
            id: 22,

          },
          {
            name: 'Camry Cars',
            description: 'Built differently',
            price: 49.99,
            quantity: 48,
            id: 23,

          },
         
    ],
    searchQuery: '', 
    selectedProduct: null, // Currently selected product based on search
    pageSize: 8, // Number of products per page
    currentPage: 1, // Current page number


  }
  },
  created() {
       
        // Retrieve current page from localStorage on component creation
        const savedPage = localStorage.getItem('currentPage');
        if (savedPage) {
          this.currentPage = parseInt(savedPage);
        }
        const sortingPreference = localStorage.getItem('sortingPreference');
        if (sortingPreference) {
          // Sort products based on the saved sorting preference
          if (sortingPreference === 'asc') {
            this.sortProductsByPriceInAscendingOrder();
          } else if (sortingPreference === 'desc') {
            this.sortProductsByPriceInDescendingOrder();
          }
          }
    },
   
  computed: {

     // Filtered products based on search query
    filteredProducts() {
      return this.products.filter(item =>
      item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    // Search suggestions based on search query
    searchSuggestions() {
      if (!this.searchQuery) return [];
      const regex = new RegExp(this.searchQuery, 'i');
      return this.products.filter(product => regex.test(product.name));
    },
      // Calculate the total number of pages needed
        totalPages() {
          return Math.ceil(this.products.length / this.pageSize);
        },
        // Slice the products array to display products for the current page
        displayedProducts() {
          const startIndex = (this.currentPage - 1) * this.pageSize;
          const endIndex = startIndex + this.pageSize;
          return this.products.slice(startIndex, endIndex);
        },
  },
  watch: {
        // Watch for changes in searchQuery and find the matching product
        searchQuery(newValue) {
          this.selectedProduct = this.findProductByName(newValue);
        },
        // Watch for changes in the current page and save it to localStorage
         currentPage(newPage) {
          localStorage.setItem('currentPage', newPage.toString());
        },
      },
  methods: {
  findProductByName(name) {
          return this.products.find(item =>
            item.name.toLowerCase() === name.toLowerCase())
          },
    
     // Method to sort products by price in ascending order and save the sorting preference in localStorage
     sortProductsByPriceInAscendingOrder() {
      this.products.sort((a, b) => a.price - b.price);
      localStorage.setItem('sortingPreference', 'asc');
    },
    // Method to sort products by price in descending order and save the sorting preference in localStorage
    sortProductsByPriceInDescendingOrder() {
      this.products.sort((a, b) => b.price - a.price);
      localStorage.setItem('sortingPreference', 'desc');
    },
   // Method to select a search suggestion and update the search query
   selectSuggestion(suggestion) {
      this.searchQuery = suggestion.name;
      // Clear the selected suggestion by removing it from the search suggestions array
       this.searchSuggestions = [];
    },

  // Method to navigate to the previous page
  prevPage() {
          if (this.currentPage > 1) {
            this.currentPage--;
            localStorage.setItem('currentPage', this.currentPage); // Update currentPage in localStorage

          }
        },
        // Method to navigate to the next page
        nextPage() {
          if (this.currentPage < this.totalPages) {
            this.currentPage++;
            localStorage.setItem('currentPage', this.currentPage); // Update currentPage in localStorage

          }
        },

}
}
</script>

<style scoped>

.searchQuery{
  border-radius: 10px;
  border: none;
  width: 300px;
}

.searchQuery::placeholder{
  color: lightblue;
  font-weight: bolder;
  position: relative;
  left: 10px;
}

.sortButtons{
  margin-top: 1.4rem;
}
.ascButton{
  margin-right: 0.6rem;
  border-radius: 10px;
  border: none;
  width: 200px;
}
.desButton{
  margin-left: 0.6rem;
  border-radius: 10px;
  border: none;
  width: 200px;
}
.PageButtonDiv{
  margin-top: 1.2rem;
}
.PageButton{
  border-radius: 10px;
  border: none;
  width: 100px;

}
.search-suggestions {
  list-style: none;
  padding: 0;
  margin: 0;
}

.search-suggestions li {
  cursor: pointer;
  padding: 5px;
}

.search-suggestions li:hover {
  color: lightcoral;
  font-weight: bolder;
}
</style>
