<template>
    <div class="courses">
        <!-- <h2>這是搜尋結果頁</h2> -->
        <div class="search_bar">
            <router-link to="/#">   
                <a class="pre" href=""><img src="../assets/img/pre.png" alt=""></a>
            </router-link>
            <input type="text" class="search" placeholder="">
            <div class="flowers">
                <img class="flowers flower1" src="../assets/img/flower1.png" alt="">
                <img class="flowers flower2" src="../assets/img/flower2.png" alt="">
            </div>
        </div>
        <!-- <div class="filter">
            <p>搜尋結果</p>
            <button type="button" class="">星級</button>
            <button type="button" class="">更新時間</button>
        </div> -->
        <div class="course-list">
            <p>搜尋結果</p>
            <div class="card" v-for="item in course" :key="item.id">
                <div class="card-body">
                    <div class="card-content">
                        <h5 class="card-title">{{item.courseName}}</h5>
                        <p class="card-text"><small class="text-muted">{{item.teacherName}}  老師</small></p>
                    </div>
                    <div class="value">
                        <p class='star_value'>{{item.starLevel}}</p>
                        <div class="ratings">
                            <div class="empty_star">★★★★★</div>
                            <div class="full_star" v-bind:style="{width: item.starLevel * 20 + '%'}">★★★★★</div>
                        </div>
                    </div>
                    <router-link :to= "`/evaluationList/${item.id}`">
                        <div class="see-more">
                            <a href="" @click="getEva(item.pid)"><img src="../assets/img/seemore.png" alt=""></a>
                        </div>
                    </router-link>
                    <!-- <button  class="see-more" type="button" @click="getEva(item.id)"><img src="../assets/img/seemore.png" alt=""></button> -->
                </div>
            </div>
            <router-link to="/newCourse">
                <div class="new_course">
                    <img src="../assets/img/newCourse.png" alt="">
                    <p>新增課程</p>
                </div>
            </router-link>
        </div>
        <footer>
            <p>made by utaipei student. 2020</p>
            <div class="footer_bar"></div>
      </footer>
    </div>
</template>

<script>
export default {
  name: 'course',
  data() {
    return {
      course: [],
    };
  },
  methods: {
      getEva(id) {
      this.$router.push(`/evaluationList/${id}`);
    },
  },
//   created() {
//     const url = `http://163.21.235.164:8080/courseList/設`;
//     this.$http.get(url)
//       .then((res) => {
//         console.log(res);
//         this.course = res.data;
        
//         // console.log(this.course);
//         // console.log(this.course.courseName);
//         // console.log(this.course.teacherName);
//       });
//   },
// };
created() {
        const { key } = this.$route.params;
        const url = `http://163.21.235.164:8080/courseList/${key}`;
        console.log(this.$route.params);
        this.$http.get(url)
        .then((res) => {
            console.log(res);
            this.course = res.data;
        });
    },
};
</script>
