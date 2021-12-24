<template>
  <h2 class="my-2 text-2xl font-bold text-gray-700 dark:text-gray-200">
    Auction Details
  </h2>
  <div v-for="(auction, index) in auctions" :key="auction.id">
    <div class="flex flex-col md:flex-row -mx-4">
      <tr>
        <td class="px-3 py-3 text-xs text-center">
          <div class="w-60">
            <img class="w-50 h-60" :src="path + auction.front_image" />
            <span
              class="
                class=mb-1
                font-semibold
                text-gray-800 text-xl
                md:text-xl
                mx-10
              "
              >Front Image</span
            >
          </div>
        </td>
        <td class="px-3 py-3 text-xs text-center">
          <div class="w-60">
            <img class="w-50 h-60" :src="path + auction.back_image" />
            <span
              class="
                class=mb-1
                font-semibold
                text-gray-800 text-xl
                md:text-xl
                mx-10
              "
              >Back Image</span
            >
          </div>
        </td>
        <td class="px-3 py-3 text-xs text-center">
          <div class="w-60">
            <img class="w-50 h-60" :src="path + auction.left_image" />
            <span
              class="
                class=mb-1
                font-semibold
                text-gray-800 text-xl
                md:text-xl
                mx-10
              "
              >Left Image</span
            >
          </div>
        </td>
        <td class="px-3 py-3 text-xs text-center">
          <div class="w-60">
            <img class="w-50 h-60" :src="path + auction.right_image" />
            <span
              class="
                class=mb-1
                font-semibold
                text-gray-800 text-xl
                md:text-xl
                mx-10
              "
              >Right Image</span
            >
          </div>
          <br />
        </td>

        <div class="md:flex-1 px-4">
          <span class="class=mb-2 font-bold text-gray-700 text-2xl md:text-2xl"
            >Product Name: {{ auction.product_name }}</span
          ><br />
          <p
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Description:
          </p>
          <p class="text-gray-800">{{ auction.description }}</p>
          <h2
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Product Price: {{ auction.base_price }}
          </h2>
          <h2
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Auction Start Date: {{ auction.start_time }}
          </h2>
          <h2
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Auction Close Date: {{ auction.close_time }}
          </h2>
          <h2
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Winner Bid: {{ auction.winner_bid }}
          </h2>
          <h2
            class="
              class=mb-2
              mt-2
              font-semibold
              text-gray-800 text-xl
              md:text-xl
            "
          >
            Winner's Name: {{ auction.name }}
          </h2>
        </div>
      </tr>
    </div>
  </div>
</template>

<script>
import AuctionService from "../../../services/AuctionService";
export default {
  data() {
    return {
      auctions: {},
      auctionid: this.$route.params.id,
      image: 1,
      path: "http://127.0.0.1:8000/",
    };
  },
  created() {
    this.getauctiondetails();
  },
  methods: {
    getauctiondetails() {
      AuctionService.getauctiondetails(this.auctionid)
        .then((response) => {
          this.auctions = response.data.data;
          console.log(this.auctions);
        })
        .catch((response) => {
          this.errors = response.error.data;
        });
    },
  },
};
</script>