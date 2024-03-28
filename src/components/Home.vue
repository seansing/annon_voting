<template>
  <main role="main">
    <!-- header -->
    <div class="container">
      <header
        class="d-flex flex-wrap align-items-center justify-content-center justify-content-md-between py-3 mb-4 border-bottom">
        <a href="/" class="d-flex align-items-center text-dark text-decoration-none">
          <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="currentColor"
            class="bi bi-bootstrap-fill d-inline-block me-2" viewBox="0 0 16 16">
            <path
              d="M6.375 7.125V4.658h1.78c.973 0 1.542.457 1.542 1.237 0 .802-.604 1.23-1.764 1.23H6.375zm0 3.762h1.898c1.184 0 1.81-.48 1.81-1.377 0-.885-.65-1.348-1.886-1.348H6.375v2.725z" />
            <path
              d="M4.002 0a4 4 0 0 0-4 4v8a4 4 0 0 0 4 4h8a4 4 0 0 0 4-4V4a4 4 0 0 0-4-4h-8zm1.06 12V3.545h3.399c1.587 0 2.543.809 2.543 2.11 0 .884-.65 1.675-1.483 1.816v.1c1.143.117 1.904.931 1.904 2.033 0 1.488-1.084 2.396-2.888 2.396H5.062z" />
          </svg>
          <span>Class Monitor Election Voting System</span>
        </a>
        <ul class="nav col-12 col-md-auto mb-2 justify-content-center mb-md-0">
          <li><a href="#/vote" class="btn btn-info">Vote</a></li>
        </ul>

        <div class="col-md-3 text-end">
          <a class="btn btn-outline-primary me-2" href="#/results" target="_blank" rel="noopener">Results</a>
          <a class="btn btn-outline-primary me-2" href="#/validator" target="_blank" rel="noopener">Validate</a>
          <a class="btn btn-primary" href="#/registration" target="_blank" rel="noopener">Register</a>
        </div>
      </header>

      <div class="py-4 px-3 mx-auto">
        <!-- result -->
        <ul class="list-group">
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Wang Tian Yang:</div>
              "Dedicated to fostering unity and amplifying student voices, I vow to lead with empathy and
              innovation as your class monitor."
            </div>
            <!--<span class="badge bg-primary rounded-pill"> {{ options[0] }}</span>-->
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Ma Le Xin:</div>
              "Committed to inclusivity and positive change, I aspire to create an environment where every
              student's ideas are valued and heard, making our class stronger together."
            </div>
            <!--<span class="badge bg-primary rounded-pill"> {{ options[1] }}</span>-->
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Wang Chen Xin:</div>
              "Driven by a passion for collaboration and growth, I promise to work tirelessly to enhance our
              class experience, ensuring that each voice is not just heard, but truly considered."
            </div>
            <!--<span class="badge bg-primary rounded-pill"> {{ options[2] }}</span>-->
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Wang Guan Zhong:</div>
              "With a focus on integrity and service, I am dedicated to representing our class with transparency
              and accountability, striving to make our shared journey through school memorable and meaningful."
            </div>
            <!--<span class="badge bg-primary rounded-pill"> {{ options[3] }}</span>-->
          </li>
        </ul>
        <!-- result -->
        <!-- <hr class="col-1 my-5 mx-0"> -->
        <!-- <a href="#/registration" class="btn btn-primary">Registration to vote</a> -->
        <!-- <a href="#/vote" class="btn btn-primary">Vote</a> -->
        <!-- <a href="#/results" class="btn btn-primary">Results</a> -->
      </div>

      <hr class="mt-5 mb-4">
      <p class="text-muted">Empowering class monitor elections with a secure and transparent voting system, utilizing
        zero-knowledge proofs and blockchain technology for confidentiality and integrity.</p>
    </div>
  </main>
</template>

<script lang="ts">
import { Component, Vue } from "vue-facing-decorator";
import * as ethers from "ethers";

@Component
export default class Home extends Vue {
  public options = [0, 0, 0, 0];

  mounted() {
    this.init();
  }

  async init() {
    const abi = [
      "function getOptionCounter(uint _option) external view returns (uint)",
    ];
    const provider = new ethers.providers.Web3Provider(
      (window as any).ethereum
    );
    const signer = provider.getSigner();
    const contracts = await (await fetch("contracts.json")).json();
    const contract = new ethers.Contract(contracts.zktreevote, abi, signer);
    for (let i = 0; i < 4; i++) {
      this.options[i] = (await contract.getOptionCounter(i + 1)).toString();
    }
    console.log(this.options[3]);
  }
}
</script>