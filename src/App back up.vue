<script setup>
import { ref } from 'vue'

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
      <div v-else class="placeholder-page">
        <div class="placeholder-icon">
          {{ activePage === 'Marketplace' ? '🛍️' : activePage === 'Earn' ? '✦' : activePage === 'Campus Rides' ? '🚗' : '💬' }}
        </div>
        <p class="section-kicker">CAMPUSLOOP</p>
        <h1>{{ activePage }}</h1>
        <p>This section is part of the interactive prototype.</p>
        <button class="primary-button" @click="goTo('Dashboard')">← Back to dashboard</button>
      </div>

    </main>
  </div>
</template>