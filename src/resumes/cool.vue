<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div v-if="person.birth" class="banner__location">{{ lang.born }} {{person.birth.day}}  {{person.birth.month}} {{person.birth.year}} {{ lang.bornIn }} {{person.birth.location}}</div>
      
    </div>

    <div class="content">
      <div class="content__left">

  <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>
          <br/>
          <div class="section-content section-content--plain">
            <div class="section-link">
              <i class="section-link__icon material-icons">business</i>{{ person.contact.street }}
            </div>
             <br/>
            <a
              class="section-link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>
            <br/>
            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}<br/>
            </div>
            <br/>
            <a
              v-if="person.contact.website"
              class="section-link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>
            <br/>
            <a
              v-if="person.contact.linkedin"
              class="section-link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>
            <br/>
            <a
              v-if="person.contact.github"
              class="section-link"
              :href="contactLinks.github"
              target="_black"
              >
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>
            
            <a
              v-if="person.contact.medium"
              class="section-link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>
        </div>
<br/>
 
    <div class="item last">
      <div class="section-headline">
        {{ lang.skills }}
      </div>
      <div class="skill" v-for="skill in person.skills" :key="skill.name">
        <div class="right">
          <span>{{skill.name}}&nbsp;</span>
          <div class="progress">
            <div class="determinate" :style="'width: '+skill.level+'%;'">
              <i class="fa fa-circle"></i>
            </div>
          </div>
        </div>
      </div>
    </div>


            </div>

      <div class="content__right">
        
 
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>
   
       <div class="section-content">
          <a v-for="(experience, index) in person.experience" :key="index"
            class="section-content__item"
            :href="experience.website">

            <span class="section-content__header"> {{ experience.position }} -  <span class="anchar"><a v-bind:href="''+experience.website+''"  target="_blank">{{experience.company}}</a></span></span>
            <div class="section-content__text"> {{ experience.timeperiod }} </div>
            <span class="section-content__text"> {{ experience.description }} </span>
          </a>
        </div>
        </div>

      
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>
                  <div class="section-content">
          <a v-for="(education, index) in person.education" :key="index"
            class="section-content__item"
            :href="education.website">

            <span class="section-content__header"> {{ education.school }}</span>
            <span class="section-content__subheader">{{ education.degree }} -  <span class="anchar"><a v-bind:href="''+education.website+''"  target="_blank">{{education.name}}</a></span></span>
            <span class="section-content__text"> {{ education.timeperiod }} </span>
            <span class="section-content__text--light"> {{ education.description }} </span>
          </a>
        </div>
          
        </div>
      </div>
    </div>

    <img class="picture"/>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'cool';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #34495E;
@banner-color: #34495E;
@banner-height: 120px;
@picture-size: 120px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.anchar{
  color: blue;
  font-size: 12px;
 
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  /*
    background-image: url('../../resume/banner.png');
    background-repeat: no-repeat;
    background-size: cover;
  */
  color: white;

  &__fullname {
    font-size: 32px;
  }

  &__position {
    font-size: 16px;
  }

  &__location {
    font-size: 12px;
  }
}
.section-content {
  margin-top: 10px;
  padding-left: 32px;
}

.section-content__item {
  display: block;
  margin-bottom: 10px;
}

.section-content__item-grid {
  flex: 1 1 0;

  margin-bottom: 10px;
  padding-right: 10px;
}

.section-content__subheader,
.section-content__text--light,
.section-content__header {
  line-height: 1.5em;
}

.section-content__text {
  display: block;
  font-weight: 300;
}


.section-content__text--light {
  color: rgba(0,0,0,0.42);
  font-weight: 300;
}

.section-content__header {
  display: block;

  font-size: 1.1em;
  font-weight: 500;
}


.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
      text-transform: uppercase;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 20px 0;
  
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;

  &__icon {
    color: white;
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__item {
    display: block;
    margin-bottom: 5px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  color: white;
  margin-top: 5px;
  padding: 5px;
}

    .skill {
      clear:both;
      width:97%;
      padding-top:4px;
      .left {
        float:left;
        width:10%;
        padding-top:3px;
        i:nth-child(2) {
          float:left;
          padding-top:4px;
        }
      }
      .right {
        
        width:93%;
        .progress {
          float:left;
          position:relative;
          height:2px;
          display:block;
          width:95%;
          background-color:rgba(255,255,255,0.19);
          border-radius:2px;
          margin:0.5rem 0 1rem;
          overflow:visible;
          margin-bottom:10px;
          .determinate {
            background-color:#78909c;
            position:absolute;
            top:0;
            bottom:0;
            .fa, .material-icons {
              font-size:13px;
              position:absolute;
              top:-4px;
              right:-2px;
              margin-left:50%;
              color:white;
            }
          }
        }
      }
    }

</style>
