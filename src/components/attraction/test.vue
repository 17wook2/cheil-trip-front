<script setup>
import { ref,onMounted, onBeforeUpdate, onBeforeMount } from 'vue';
import { getsearchOptionList, getKeywordAttractionList, getAreaBasedAttractionList } from '@/api/AttractionAPI.js'
import AttractionListRow from "./AttractionListRow.vue";
let searchOptions = ref([]);
const areaCode = ref(0);
const contentTypeId = ref(0);
const keyword = ref("");
const tripList = ref([]);
onMounted(async() => {
    searchOptions.value = await getsearchOptionList();
    console.log(searchOptions);
})

async function searchAttraction() {
    const params = { listYN: 'Y', arrange : 'A', numOfRows : 10, pageNo : 1}
    if (areaCode.value != 0) params.areaCode = areaCode.value
    if (contentTypeId.value != 0) params.contentTypeId = contentTypeId.value
    if (keyword.value != null && keyword.value.length > 0) {
        params.keyword = keyword.value
        tripList.value = await getKeywordAttractionList(params)
    } else {
        tripList.value = await getAreaBasedAttractionList(params)
    }
    console.log(tripList.value)
}

</script>

<template>
    <form>
    <div v-for="searchOption in searchOptions" 
        :key="searchOption.rnum" 
        :value="searchOption.code">{{searchOption.name}}</div>
    <select class="form-select me-2" v-model="areaCode">
        <option v-for="searchOption in searchOptions" 
        :key="searchOption.rnum" 
        :value="searchOption.code">{{searchOption.name}}</option>
    </select> 
    <select class="form-select me-2" v-model="contentTypeId">
                    <option value="0" selected>관광지 유형</option>
                    <option value="12">관광지</option>
                    <option value="14">문화시설</option>
                    <option value="15">축제공연행사</option>
                    <option value="25">여행코스</option>
                    <option value="28">레포츠</option>
                    <option value="32">숙박</option>
                    <option value="38">쇼핑</option>
                    <option value="39">음식점</option>
                </select>
    <input
                        id="search-keyword"
                        class="form-control me-2"
                        type="search"
                        placeholder="검색어"
                        aria-label="검색어"
                        v-model="keyword"
                />
                <button id="btn-search" class="btn btn-outline-success" type="button" @click="searchAttraction">검색</button>
    </form>
    <div class="row col-6">
            <table class="table table-striped">
                <thead>
                <tr>
                    <th>대표이미지</th>
                    <th>관광지명</th>
                    <th>주소</th>
                    <th>위도</th>
                    <th>경도</th>
                </tr>
                </thead>
                <attraction-list-row v-for="trip in tripList" :key="trip.contentid" v-bind= "trip"/>
            </table>
    </div>
</template>

<style scoped>

</style>