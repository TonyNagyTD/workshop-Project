<!-- eslint-disable vue/no-parsing-error -->
<template>
  <div class="list-component">
    <!-- Your component content here -->
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div class="filter-bar"  v-if=" tags.length > 0">
            <div class="filter-bar__tag-input">
              <div
                v-for="(tag, index) in tags"
                :key="tag"
                class="tag-input__tag"
              >
                {{ tag }}
                <span @click="removeTag(index)">x</span>
              </div>
            </div>
            <div class="clear-btn">
              <button class="clear-btn--style" type="button" @click="clearTags">Clear</button>
            </div>
          </div>
        </div>
        <div class="col-md-12">
          <div class="card-list" v-for="lists in list" :key="lists.id">
            <div class="card-list__card-body">
              <div class="row">
                <div class="col-md-6">
                  <div class="left-side">
                    <div class="left-side__img">
                      <img class="left-side__img__style" src="../../assets/imgs/account.svg" alt="" />
                    </div>
                    <div class="left-side__info">
                      <div class="left-side__info__name">
                        <div class="left-side__info__title">
                          <h2 class="left-side__info__title__h2">
                            {{ lists.company }}
                          </h2>
                        </div>
                        <div class="left-side__info__tags">
                          <button
                            v-if="lists.new"
                            type="button"
                            class="left-side__info__tags__Btn"
                          >
                            NEW!
                          </button>
                          <button
                            v-if="lists.featured"
                            type="button"
                            class="left-side__info__tags__Btn left-side__info__tags__Btn--black"
                          >
                            FEATURED
                          </button>
                        </div>
                      </div>
                      <div class="left-side__info__position">
                        <h2 class="left-side__info__position__h2">
                          {{ lists.position }}
                        </h2>
                      </div>
                      <div class="left-side__info__contact-info">
                        <p class="contact-info__prag">{{ lists.postedAt }}</p>
                        <p class="contact-info__prag">{{ lists.contract }}</p>
                        <p class="contact-info__prag">{{ lists.location }}</p>
                      </div>
                    </div>
                  </div>
                  <div class="seperator"></div>
                </div>
                <div class="col-md-6">
                  <div class="right-side">
                    <div class="right-side__filter-tags">
                      <button
                        type="button"
                        class="right-side__filter-tags__btns"
                        v-for="(language, index) in lists.languages"
                        :key="index"
                        @click="filterByLanguage(language)"
                      >
                        {{ language }}
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import listData from '../../data.json'

export default {
  name: 'ListComponent',
  data () {
    return {
      tags: [],
      list: listData,
      showFilterBar: true
    }
  },
  methods: {
    removeTag (index) {
      this.tags.splice(index, 1)

      if (this.tags.length > 0) {
        this.list = listData.filter(item =>
          this.tags.some(tag => item.languages.includes(tag))
        )
      } else {
        this.list = listData
      }
    },
    filterByLanguage (selectedLanguage) {
    // Toggle the selected language in the tags array
      if (this.tags.includes(selectedLanguage)) {
      // If the language is already selected, remove it
        this.tags = this.tags.filter(tag => tag !== selectedLanguage)
      } else {
      // If the language is not selected, add it
        this.tags.push(selectedLanguage)
      }

      // If there are selected tags, filter the list; otherwise, show all data
      if (this.tags.length > 0) {
        this.list = listData.filter(item =>
          this.tags.every(tag => item.languages.includes(tag))
        )
      } else {
      // If no tags are selected, show all data
        this.list = listData
      }
    },
    clearTags () {
      this.tags = []
      this.list = listData // Reset the list to show all data
      this.showFilterBar = false // Add a data property to control filter bar visibility
    }
  }
}
</script>

<style lang="scss">
@import "./List-component.scss";
</style>
