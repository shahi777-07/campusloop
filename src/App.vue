<script setup>
import { ref , computed } from 'vue'

const activePage = ref('Dashboard')

const navItems = [
  { name: 'Dashboard', icon: '⌂' },
  { name: 'Marketplace', icon: '🛍' },
  { name: 'Earn', icon: '✦' },
  { name: 'Campus Rides', icon: '🚗' },
  { name: 'Messages', icon: '💬' }
]

const products = [
  { title: 'Casio Scientific Calculator', category: 'Study Essentials', price: '₹650', oldPrice: '₹1,250', seller: 'Arjun • 3rd Year', icon: '🧮', tag: 'Good deal' },
  { title: 'Engineering Mathematics Notes', category: 'Study Materials', price: '₹120', oldPrice: '', seller: 'Meera • 2nd Year', icon: '📚', tag: 'Popular' },
  { title: 'HP Laptop Backpack', category: 'Accessories', price: '₹450', oldPrice: '₹900', seller: 'Rahul • 4th Year', icon: '🎒', tag: '50% off' }
]

const gigs = [
  { title: 'Short-form Video Editing', client: 'Verified Client', budget: '₹800–₹2,000', icon: '🎬', color: 'purple' },
  { title: 'Poster & Social Media Design', client: 'Campus Club', budget: '₹500–₹1,500', icon: '🎨', color: 'orange' },
  { title: 'Website / Project Help', client: 'Verified Student', budget: '₹1,000–₹4,000', icon: '💻', color: 'blue' }
]

const rides = [
  { from: 'Kollam', to: 'Campus', time: '8:15 AM', driver: 'Adithya', seats: '2 seats', cost: '₹30' },
  { from: 'Karunagappally', to: 'Campus', time: '8:30 AM', driver: 'Nikhil', seats: '1 seat', cost: '₹40' }
]

const marketSearch = ref('')
const marketCategory = ref('All')
const selectedProduct = ref(null)
const showPostModal = ref(false)
const savedProducts = ref([])

const categories = [
  'All',
  'Study Essentials',
  'Study Materials',
  'Accessories',
  'Electronics',
  'Hostel',
  'Sports'
]

const marketplaceProducts = [
  ...products,
  {
    title: 'Wireless Headphones',
    category: 'Electronics',
    price: '₹850',
    oldPrice: '₹1,500',
    seller: 'Dev • 3rd Year',
    icon: '🎧',
    tag: 'Great deal'
  },
  {
    title: 'Lab Coat',
    category: 'Study Essentials',
    price: '₹300',
    oldPrice: '₹650',
    seller: 'Anjali • 2nd Year',
    icon: '🥼',
    tag: 'Like new'
  },
  {
    title: 'Hostel Study Lamp',
    category: 'Hostel',
    price: '₹250',
    oldPrice: '₹500',
    seller: 'Fahad • 4th Year',
    icon: '💡',
    tag: 'Popular'
  }
]

const filteredProducts = computed(() => {
  return marketplaceProducts.filter(product => {
    const matchesSearch =
      product.title.toLowerCase().includes(marketSearch.value.toLowerCase()) ||
      product.category.toLowerCase().includes(marketSearch.value.toLowerCase())

    const matchesCategory =
      marketCategory.value === 'All' ||
      product.category === marketCategory.value

    return matchesSearch && matchesCategory
  })
})

function openProduct(product) {
  selectedProduct.value = product
}

function closeProduct() {
  selectedProduct.value = null
}

function toggleSave(product) {
  if (savedProducts.value.includes(product.title)) {
    savedProducts.value = savedProducts.value.filter(
      title => title !== product.title
    )
  } else {
    savedProducts.value.push(product.title)
  }
}

function contactSeller(product) {
  selectedProduct.value = null
  activePage.value = 'Messages'
  alert(`Message started with ${product.seller.split(' • ')[0]}!`)
}
function goTo(page) {
  activePage.value = page
}

function actionMessage(message) {
  alert(message)
}
</script>

<template>
  <div class="app-shell">

    <!-- SIDEBAR -->
    <aside class="sidebar">
      <div class="brand">
        <div class="brand-mark">C</div>
        <div>
          <div class="brand-name">Campus<span>Loop</span></div>
          <div class="brand-sub">Student ecosystem</div>
        </div>
      </div>

      <div class="college-card">
        <div class="college-icon">🎓</div>
        <div>
          <strong>Verified Student</strong>
          <span>College ID verified</span>
        </div>
        <div class="verified">✓</div>
      </div>

      <nav>
        <p class="nav-label">WORKSPACE</p>

        <button
          v-for="item in navItems"
          :key="item.name"
          :class="['nav-item', { active: activePage === item.name }]"
          @click="goTo(item.name)"
        >
          <span class="nav-icon">{{ item.icon }}</span>
          <span>{{ item.name }}</span>
          <span v-if="item.name === 'Messages'" class="notification">3</span>
        </button>

        <p class="nav-label second">ACCOUNT</p>

        <button class="nav-item" @click="actionMessage('Profile & verification coming next!')">
          <span class="nav-icon">◉</span>
          <span>My Profile</span>
        </button>

        <button class="nav-item" @click="actionMessage('Your earnings dashboard is coming next!')">
          <span class="nav-icon">₹</span>
          <span>My Earnings</span>
        </button>
      </nav>

      <div class="sidebar-bottom">
        <div class="help-card">
          <div class="help-icon">?</div>
          <div>
            <strong>Need help?</strong>
            <span>We're here for you.</span>
          </div>
        </div>

        <div class="user-mini">
          <div class="avatar">AS</div>
          <div class="user-info">
            <strong>Adarsh S.</strong>
            <span>Computer Science</span>
          </div>
          <span class="more">•••</span>
        </div>
      </div>
    </aside>

    <!-- MAIN -->
    <main class="main">

      <!-- TOP BAR -->
      <header class="topbar">
        <div class="mobile-brand">Campus<span>Loop</span></div>

        <div class="search">
          <span>⌕</span>
          <input placeholder="Search products, gigs, rides..." />
          <kbd>⌘ K</kbd>
        </div>

        <div class="top-actions">
          <button class="icon-button" @click="actionMessage('You have 3 new notifications')">🔔<i></i></button>
          <button class="profile-button">
            <div class="avatar small">AS</div>
            <span>Adarsh</span>
            <b>⌄</b>
          </button>
        </div>
      </header>

      <!-- DASHBOARD -->
      <div v-if="activePage === 'Dashboard'" class="content">

        <section class="welcome">
          <div>
            <p class="eyebrow">THURSDAY, SEPTEMBER 10</p>
            <h1>Good evening, Adarsh <span>👋</span></h1>
            <p class="welcome-text">Turn what you have and what you know into opportunities.</p>
          </div>
          <button class="primary-button" @click="goTo('Earn')">+ Post an opportunity</button>
        </section>

        <!-- HERO -->
        <section class="hero">
          <div class="hero-content">
            <div class="hero-badge">THE STUDENT ECONOMY</div>
            <h2>Your campus can<br /><em>work for you.</em></h2>
            <p>
              Buy what you need. Sell what you don't.
              Earn from your skills. Share rides and expenses.
            </p>

            <div class="hero-buttons">
              <button class="hero-primary" @click="goTo('Marketplace')">Explore marketplace →</button>
              <button class="hero-secondary" @click="goTo('Earn')">Start earning</button>
            </div>
          </div>

          <div class="hero-visual">
            <div class="orbit orbit-one"></div>
            <div class="orbit orbit-two"></div>
            <div class="visual-card card-one">
              <span>💰</span>
              <div><b>₹2,450</b><small>earned this month</small></div>
            </div>
            <div class="visual-card card-two">
              <span>🛍️</span>
              <div><b>Buy & Sell</b><small>within your campus</small></div>
            </div>
            <div class="visual-card card-three">
              <span>🚗</span>
              <div><b>Share a ride</b><small>split the fuel cost</small></div>
            </div>
            <div class="hero-circle">
              <div class="circle-inner">C<span>L</span></div>
            </div>
          </div>
        </section>

        <!-- STATS -->
        <section class="stats">
          <div class="stat">
            <div class="stat-icon green">₹</div>
            <div>
              <span>MY EARNINGS</span>
              <strong>₹2,450</strong>
              <small class="positive">↑ 18% this month</small>
            </div>
          </div>

          <div class="stat">
            <div class="stat-icon purple">✦</div>
            <div>
              <span>AVAILABLE GIGS</span>
              <strong>128</strong>
              <small>Across your skills</small>
            </div>
          </div>

          <div class="stat">
            <div class="stat-icon orange">🚗</div>
            <div>
              <span>RIDE SAVINGS</span>
              <strong>₹680</strong>
              <small class="positive">Saved this month</small>
            </div>
          </div>

          <div class="stat">
            <div class="stat-icon blue">♢</div>
            <div>
              <span>TRUST SCORE</span>
              <strong>4.9 <small>/ 5</small></strong>
              <small>Excellent reputation</small>
            </div>
          </div>
        </section>

        <!-- LOWER GRID -->
        <div class="section-grid">

          <!-- MARKETPLACE -->
          <section class="panel marketplace-panel">
            <div class="panel-heading">
              <div>
                <p class="section-kicker">CAMPUS MARKETPLACE</p>
                <h3>Find useful stuff nearby</h3>
              </div>
              <button class="text-button" @click="goTo('Marketplace')">View all →</button>
            </div>

            <div class="product-list">
              <div v-for="product in products" :key="product.title" class="product">
                <div class="product-image">{{ product.icon }}</div>
                <div class="product-info">
                  <span class="product-tag">{{ product.tag }}</span>
                  <h4>{{ product.title }}</h4>
                  <p>{{ product.seller }}</p>
                  <div>
                    <b>{{ product.price }}</b>
                    <del v-if="product.oldPrice">{{ product.oldPrice }}</del>
                  </div>
                </div>
                <button class="round-arrow" @click="actionMessage('Product details opened!')">↗</button>
              </div>
            </div>
          </section>

          <!-- EARN -->
          <section class="panel earn-panel">
            <div class="panel-heading">
              <div>
                <p class="section-kicker">EARN WITH YOUR SKILLS</p>
                <h3>Opportunities for you</h3>
              </div>
              <button class="text-button" @click="goTo('Earn')">Explore →</button>
            </div>

            <div class="gig-list">
              <div v-for="gig in gigs" :key="gig.title" class="gig">
                <div :class="['gig-icon', gig.color]">{{ gig.icon }}</div>
                <div class="gig-info">
                  <h4>{{ gig.title }}</h4>
                  <p>✓ {{ gig.client }}</p>
                </div>
                <strong>{{ gig.budget }}</strong>
              </div>
            </div>

            <div class="earn-banner">
              <div>
                <b>Have a skill others need?</b>
                <span>Turn your free hours into income.</span>
              </div>
              <button @click="actionMessage('Create your first gig!')">Create gig</button>
            </div>
          </section>
        </div>

        <!-- RIDE SECTION -->
        <section class="panel ride-panel">
          <div class="panel-heading">
            <div>
              <p class="section-kicker">CAMPUS RIDE SHARE</p>
              <h3>Going your way?</h3>
            </div>
            <button class="text-button" @click="goTo('Campus Rides')">See all rides →</button>
          </div>

          <div class="ride-content">
            <div class="route-visual">
              <div class="route-dot"></div>
              <div class="route-line"></div>
              <div class="route-dot end"></div>
              <div class="route-label start">Kollam</div>
              <div class="route-label finish">Campus</div>
            </div>

            <div v-for="ride in rides" :key="ride.driver" class="ride-item">
              <div class="ride-time">{{ ride.time }}</div>
              <div class="ride-driver">
                <div class="avatar ride-avatar">{{ ride.driver[0] }}</div>
                <div>
                  <b>{{ ride.driver }}</b>
                  <span>{{ ride.from }} → {{ ride.to }}</span>
                </div>
              </div>
              <span class="seat-pill">{{ ride.seats }}</span>
              <strong>{{ ride.cost }}</strong>
              <button class="join-button" @click="actionMessage('Ride request sent!')">Join ride</button>
            </div>
          </div>
        </section>

        <footer>
          <span>CampusLoop © 2026</span>
          <span>Built for students, by students.</span>
          <span>🔐 Safety & verification first</span>
        </footer>
      </div>

      <!-- OTHER PAGES -->

<!-- MARKETPLACE -->
<div v-else-if="activePage === 'Marketplace'" class="marketplace-page">

  <section class="marketplace-header">
    <div>
      <p class="section-kicker">CAMPUS MARKETPLACE</p>
      <h1>Find useful stuff nearby.</h1>
      <p>
        Buy pre-loved essentials from verified students on your campus.
      </p>
    </div>

    <button class="primary-button" @click="showPostModal = true">
      + Post an item
    </button>
  </section>

  <!-- SEARCH -->
  <div class="marketplace-tools">

    <div class="market-search">
      <span>⌕</span>
      <input
        v-model="marketSearch"
        placeholder="Search calculators, books, electronics..."
      />
    </div>

    <div class="category-scroll">
      <button
        v-for="category in categories"
        :key="category"
        :class="['category-button', { active: marketCategory === category }]"
        @click="marketCategory = category"
      >
        {{ category }}
      </button>
    </div>

  </div>

  <!-- TRUST BANNER -->
  <div class="trust-banner">
    <div class="trust-symbol">✓</div>
    <div>
      <strong>Verified student marketplace</strong>
      <span>Buy and sell with students from your campus.</span>
    </div>
    <div class="trust-points">
      <span>🔐 Verified users</span>
      <span>⭐ Ratings</span>
      <span>📍 Nearby deals</span>
    </div>
  </div>

  <!-- PRODUCTS -->
  <section class="marketplace-results">

    <div class="results-heading">
      <div>
        <p class="section-kicker">AVAILABLE NOW</p>
        <h2>{{ filteredProducts.length }} items near you</h2>
      </div>

      <span v-if="marketSearch">
        Searching for "{{ marketSearch }}"
      </span>
    </div>

    <div v-if="filteredProducts.length" class="marketplace-grid">

      <article
        v-for="product in filteredProducts"
        :key="product.title"
        class="market-card"
      >

        <div class="market-image">
          <span>{{ product.icon }}</span>

          <button
            class="save-button"
            @click.stop="toggleSave(product)"
          >
            {{ savedProducts.includes(product.title) ? '♥' : '♡' }}
          </button>

          <span class="deal-badge">
            {{ product.tag }}
          </span>
        </div>

        <div class="market-card-body">

          <span class="market-category">
            {{ product.category }}
          </span>

          <h3>{{ product.title }}</h3>

          <div class="market-price">
            <strong>{{ product.price }}</strong>
            <del v-if="product.oldPrice">{{ product.oldPrice }}</del>
          </div>

          <div class="seller-row">
            <div class="avatar tiny">
              {{ product.seller[0] }}
            </div>

            <div>
              <strong>{{ product.seller.split(' • ')[0] }}</strong>
              <span>✓ Verified student</span>
            </div>

            <span class="rating">★ 4.9</span>
          </div>

          <button
            class="view-product-button"
            @click="openProduct(product)"
          >
            View details →
          </button>

        </div>

      </article>

    </div>

    <div v-else class="empty-market">
      <div>🔎</div>
      <h3>No items found</h3>
      <p>Try another search or category.</p>
      <button
        class="primary-button"
        @click="marketSearch = ''; marketCategory = 'All'"
      >
        Clear filters
      </button>
    </div>

  </section>

  <!-- PRODUCT DETAILS MODAL -->
  <div
    v-if="selectedProduct"
    class="modal-overlay"
    @click.self="closeProduct"
  >
    <div class="product-modal">

      <button class="modal-close" @click="closeProduct">×</button>

      <div class="modal-product-image">
        {{ selectedProduct.icon }}
      </div>

      <span class="market-category">
        {{ selectedProduct.category }}
      </span>

      <h2>{{ selectedProduct.title }}</h2>

      <div class="modal-price">
        <strong>{{ selectedProduct.price }}</strong>
        <del v-if="selectedProduct.oldPrice">
          {{ selectedProduct.oldPrice }}
        </del>
      </div>

      <div class="seller-profile">
        <div class="avatar">{{ selectedProduct.seller[0] }}</div>
        <div>
          <strong>{{ selectedProduct.seller }}</strong>
          <span>✓ College ID verified · ★ 4.9 rating</span>
        </div>
      </div>

      <div class="product-info-box">
        <strong>About this listing</strong>
        <p>
          Well-maintained item available from a verified CampusLoop student.
          Meet safely on campus and inspect the item before buying.
        </p>
      </div>

      <button
        class="modal-contact-button"
        @click="contactSeller(selectedProduct)"
      >
        💬 Contact seller
      </button>

      <button class="modal-secondary-button">
        📍 Arrange campus meetup
      </button>

    </div>
  </div>

  <!-- POST ITEM MODAL -->
  <div
    v-if="showPostModal"
    class="modal-overlay"
    @click.self="showPostModal = false"
  >
    <div class="post-modal">

      <button
        class="modal-close"
        @click="showPostModal = false"
      >
        ×
      </button>

      <p class="section-kicker">SELL ON CAMPUSLOOP</p>
      <h2>Post an item</h2>
      <p class="modal-description">
        Turn something you no longer need into money for your next expense.
      </p>

      <label>Item name</label>
      <input
        class="form-input"
        placeholder="e.g. Casio calculator"
      />

      <label>Category</label>
      <select class="form-input">
        <option>Study Essentials</option>
        <option>Study Materials</option>
        <option>Electronics</option>
        <option>Accessories</option>
        <option>Hostel</option>
      </select>

      <label>Price</label>
      <input
        class="form-input"
        type="number"
        placeholder="₹ Enter price"
      />

      <label>Description</label>
      <textarea
        class="form-input"
        rows="3"
        placeholder="Tell buyers about the condition..."
      ></textarea>

      <button
        class="modal-contact-button"
        @click="showPostModal = false; alert('Your item has been added to the marketplace!')"
      >
        Publish listing →
      </button>

    </div>
  </div>

</div>

<!-- OTHER PAGES -->
<!-- MARKETPLACE -->
<div v-else-if="activePage === 'Marketplace'" class="marketplace-page">

  <div class="page-header">
    <div>
      <p class="section-kicker">CAMPUSLOOP MARKETPLACE</p>
      <h1>Buy smarter. Sell easier.</h1>
      <p class="page-subtitle">
        Discover useful items from verified students on your campus.
      </p>
    </div>

    <button class="primary-button" @click="showPostModal = true">
      + Post an item
    </button>
  </div>

  <div class="marketplace-tools">
    <div class="market-search">
      🔍
      <input
        v-model="marketSearch"
        type="text"
        placeholder="Search books, electronics, bags..."
      />
    </div>

    <div class="category-list">
      <button
        v-for="category in categories"
        :key="category"
        :class="['category-button', { active: marketCategory === category }]"
        @click="marketCategory = category"
      >
        {{ category }}
      </button>
    </div>
  </div>

  <div class="trust-banner">
    <span class="trust-icon">✓</span>
    <div>
      <strong>Shop with confidence</strong>
      <p>Connect with verified students from your campus.</p>
    </div>
  </div>

  <div class="results-heading">
    <div>
      <h2>Available near you</h2>
      <p>{{ filteredProducts.length }} items found</p>
    </div>
  </div>

  <div v-if="filteredProducts.length" class="marketplace-grid">

    <div
      v-for="product in filteredProducts"
      :key="product.title"
      class="product-card"
      @click="openProduct(product)"
    >

      <button
        class="save-button"
        @click.stop="toggleSave(product)"
      >
        {{ savedProducts.includes(product.title) ? '♥' : '♡' }}
      </button>

      <div class="product-image">
        {{ product.icon }}
      </div>

      <div class="product-info">
        <span class="product-tag">{{ product.tag }}</span>

        <h3>{{ product.title }}</h3>

        <p class="product-category">
          {{ product.category }}
        </p>

        <div class="product-price">
          <strong>{{ product.price }}</strong>
          <span v-if="product.oldPrice">
            {{ product.oldPrice }}
          </span>
        </div>

        <p class="seller">
          👤 {{ product.seller }}
        </p>
      </div>

    </div>

  </div>

  <div v-else class="empty-marketplace">
    <div>🔎</div>
    <h2>No items found</h2>
    <p>Try another search or category.</p>
  </div>

</div>

<!-- OTHER PAGES -->
<div v-else-if="activePage === 'Earn'" class="earn-page">

  <div class="page-header">
    <div>
      <p class="section-kicker">CAMPUSLOOP EARN</p>
      <h1>Turn your skills into income.</h1>
      <p class="page-subtitle">
        Find gigs, build experience and earn money on campus.
      </p>
    </div>

    <button
      class="primary-button"
      @click="actionMessage('Gig posting coming soon!')"
    >
      + Post a gig
    </button>
  </div>

  <div class="earn-stats">

    <div class="earn-stat-card">
      <span>💰</span>
      <div>
        <strong>₹4,850</strong>
        <p>Total earned</p>
      </div>
    </div>

    <div class="earn-stat-card">
      <span>💼</span>
      <div>
        <strong>8</strong>
        <p>Gigs completed</p>
      </div>
    </div>

    <div class="earn-stat-card">
      <span>⭐</span>
      <div>
        <strong>4.9</strong>
        <p>Average rating</p>
      </div>
    </div>

  </div>

  <div class="results-heading">
    <div>
      <h2>Opportunities for you</h2>
      <p>Choose a gig that matches your skills.</p>
    </div>
  </div>

  <div class="gig-grid">

    <div class="gig-card">
      <div class="gig-top">
        <span class="gig-icon">🎨</span>
        <strong>₹800</strong>
      </div>

      <span class="gig-tag">Design</span>

      <h3>Design a college event poster</h3>

      <p>Create a modern poster for a campus technical event.</p>

      <div class="gig-footer">
        <span>👤 Tech Club</span>

        <button
          class="secondary-button"
          @click="actionMessage('Application sent!')"
        >
          Apply
        </button>
      </div>
    </div>

    <div class="gig-card">
      <div class="gig-top">
        <span class="gig-icon">🎬</span>
        <strong>₹1,500</strong>
      </div>

      <span class="gig-tag">Video Editing</span>

      <h3>Edit a promotional video</h3>

      <p>Edit a short promotional video for a student startup.</p>

      <div class="gig-footer">
        <span>👤 Campus Startup</span>

        <button
          class="secondary-button"
          @click="actionMessage('Application sent!')"
        >
          Apply
        </button>
      </div>
    </div>

    <div class="gig-card">
      <div class="gig-top">
        <span class="gig-icon">💻</span>
        <strong>₹2,500</strong>
      </div>

      <span class="gig-tag">Web Development</span>

      <h3>Build a portfolio website</h3>

      <p>Create a clean one-page portfolio for a freelancer.</p>

      <div class="gig-footer">
        <span>👤 Verified Client</span>

        <button
          class="secondary-button"
          @click="actionMessage('Application sent!')"
        >
          Apply
        </button>
      </div>
    </div>

    <div class="gig-card">
      <div class="gig-top">
        <span class="gig-icon">📚</span>
        <strong>₹600</strong>
      </div>

      <span class="gig-tag">Tutoring</span>

      <h3>Teach Mathematics</h3>

      <p>Help a first-year student prepare for their exams.</p>

      <div class="gig-footer">
        <span>👤 First Year</span>

        <button
          class="secondary-button"
          @click="actionMessage('Application sent!')"
        >
          Apply
        </button>
      </div>
    </div>

  </div>

</div>

<!-- CAMPUS RIDES -->
<div v-else-if="activePage === 'Campus Rides'" class="rides-page">

  <div class="page-header">
    <div>
      <p class="section-kicker">CAMPUSLOOP RIDES</p>
      <h1>Share the ride. Split the cost.</h1>
      <p class="page-subtitle">
        Find students travelling your way and share fuel costs.
      </p>
    </div>

    <button
      class="primary-button"
      @click="actionMessage('Ride posting coming soon!')"
    >
      + Offer a ride
    </button>
  </div>

  <!-- TRUST BANNER -->
  <div class="ride-trust">
    <div class="ride-trust-icon">🛡️</div>
    <div>
      <strong>Built for trusted campus travel</strong>
      <p>
        Verified students • Transparent fuel sharing • Ratings & reviews
      </p>
    </div>
  </div>

  <!-- SEARCH -->
  <div class="ride-search-box">
    <span>🔎</span>
    <input
      type="text"
      placeholder="Search your route..."
    />
  </div>

  <!-- SECTION TITLE -->
  <div class="results-heading">
    <div>
      <h2>Rides near you</h2>
      <p>Students travelling around the same time.</p>
    </div>
  </div>

  <!-- RIDE CARDS -->
  <div class="ride-grid">

    <div class="ride-card">
      <div class="ride-top">
        <span class="ride-icon">🚗</span>
        <span class="ride-status">2 seats left</span>
      </div>

      <div class="ride-route">
        <span>Kollam</span>
        <strong>→</strong>
        <span>Trivandrum</span>
      </div>

      <div class="ride-time">
        🕐 7:30 AM
      </div>

      <div class="ride-driver">
        <div class="driver-avatar">A</div>
        <div>
          <strong>Arjun</strong>
          <span>3rd Year • ⭐ 4.9</span>
        </div>
      </div>

      <div class="ride-footer">
        <div>
          <strong>₹120</strong>
          <span> / seat</span>
        </div>

        <button
          class="secondary-button"
          @click="actionMessage('Ride request sent!')"
        >
          Join ride
        </button>
      </div>
    </div>


    <div class="ride-card">
      <div class="ride-top">
        <span class="ride-icon">🚙</span>
        <span class="ride-status">1 seat left</span>
      </div>

      <div class="ride-route">
        <span>Kottarakkara</span>
        <strong>→</strong>
        <span>Kollam</span>
      </div>

      <div class="ride-time">
        🕐 8:15 AM
      </div>

      <div class="ride-driver">
        <div class="driver-avatar">M</div>
        <div>
          <strong>Meera</strong>
          <span>2nd Year • ⭐ 4.8</span>
        </div>
      </div>

      <div class="ride-footer">
        <div>
          <strong>₹70</strong>
          <span> / seat</span>
        </div>

        <button
          class="secondary-button"
          @click="actionMessage('Ride request sent!')"
        >
          Join ride
        </button>
      </div>
    </div>


    <div class="ride-card">
      <div class="ride-top">
        <span class="ride-icon">🏎️</span>
        <span class="ride-status">3 seats left</span>
      </div>

      <div class="ride-route">
        <span>Chinnakkada</span>
        <strong>→</strong>
        <span>Campus</span>
      </div>

      <div class="ride-time">
        🕐 9:00 AM
      </div>

      <div class="ride-driver">
        <div class="driver-avatar">R</div>
        <div>
          <strong>Rahul</strong>
          <span>4th Year • ⭐ 4.9</span>
        </div>
      </div>

      <div class="ride-footer">
        <div>
          <strong>₹50</strong>
          <span> / seat</span>
        </div>

        <button
          class="secondary-button"
          @click="actionMessage('Ride request sent!')"
        >
          Join ride
        </button>
      </div>
    </div>

  </div>

</div>

<!-- FALLBACK / MESSAGES -->
<!-- MESSAGES -->
<div v-else-if="activePage === 'Messages'" class="messages-page">

  <div class="page-header">
    <div>
      <p class="section-kicker">CAMPUSLOOP MESSAGES</p>
      <h1>Stay connected.</h1>
      <p class="page-subtitle">
        Chat with students, sellers, clients and ride partners.
      </p>
    </div>

    <button
      class="primary-button"
      @click="actionMessage('New conversation coming soon!')"
    >
      + New message
    </button>
  </div>

  <div class="messages-layout">

    <!-- CONVERSATIONS -->
    <div class="conversation-panel">

      <div class="conversation-header">
        <h2>Conversations</h2>
        <span>3</span>
      </div>

      <div
        class="conversation active-conversation"
        @click="actionMessage('Chat opened with Arjun')"
      >
        <div class="message-avatar">A</div>

        <div class="conversation-info">
          <div class="conversation-name">
            <strong>Arjun</strong>
            <small>10:42 PM</small>
          </div>

          <p>Hey! Is the ride still available?</p>
        </div>

        <span class="unread-dot"></span>
      </div>


      <div
        class="conversation"
        @click="actionMessage('Chat opened with Meera')"
      >
        <div class="message-avatar">M</div>

        <div class="conversation-info">
          <div class="conversation-name">
            <strong>Meera</strong>
            <small>9:18 PM</small>
          </div>

          <p>I can share the textbook tomorrow.</p>
        </div>
      </div>


      <div
        class="conversation"
        @click="actionMessage('Chat opened with Rahul')"
      >
        <div class="message-avatar">R</div>

        <div class="conversation-info">
          <div class="conversation-name">
            <strong>Rahul</strong>
            <small>Yesterday</small>
          </div>

          <p>Thanks for the design!</p>
        </div>
      </div>


      <div
        class="conversation"
        @click="actionMessage('Chat opened with Anjali')"
      >
        <div class="message-avatar">A</div>

        <div class="conversation-info">
          <div class="conversation-name">
            <strong>Anjali</strong>
            <small>Yesterday</small>
          </div>

          <p>Is the lab coat still available?</p>
        </div>
      </div>

    </div>


    <!-- CHAT -->
    <div class="chat-panel">

      <div class="chat-header">

        <div class="chat-user">
          <div class="message-avatar large-avatar">A</div>

          <div>
            <strong>Arjun</strong>
            <span>🟢 Online • 3rd Year</span>
          </div>
        </div>

        <button
          class="chat-more"
          @click="actionMessage('More options coming soon!')"
        >
          ⋯
        </button>

      </div>


      <div class="chat-messages">

        <div class="message received">
          <p>Hey! Is the ride from Kollam to Trivandrum still available?</p>
          <span>10:39 PM</span>
        </div>

        <div class="message sent">
          <p>Yes! I still have 2 seats available.</p>
          <span>10:40 PM</span>
        </div>

        <div class="message received">
          <p>Perfect. How much is the fuel split?</p>
          <span>10:41 PM</span>
        </div>

        <div class="message sent">
          <p>₹120 per seat 👍</p>
          <span>10:42 PM</span>
        </div>

      </div>


      <div class="chat-input-area">

        <button
          class="chat-attach"
          @click="actionMessage('Attachment feature coming soon!')"
        >
          ＋
        </button>

        <input
          type="text"
          placeholder="Type a message..."
        />

        <button
          class="chat-send"
          @click="actionMessage('Message sent!')"
        >
          ➤
        </button>

      </div>

    </div>

  </div>

</div>

<!-- FALLBACK -->
<div v-else class="placeholder-page">

  <div class="placeholder-icon">
    💬
  </div>

  <p class="section-kicker">CAMPUSLOOP</p>

  <h1>{{ activePage }}</h1>

  <p>This section is part of the interactive prototype.</p>

  <button
    class="primary-button"
    @click="goTo('Dashboard')"
  >
    ← Back to dashboard
  </button>

</div>
</main>
  </div>
</template>