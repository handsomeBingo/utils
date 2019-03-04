<script>
  import lodash from 'lodash'

  let renderTmp = (d, h) => {
    return d.children ? h(
      d.tag,
      d.config,
      d.children.map((child, index) => {
        if (typeof child === 'string') {
          return child
        } else {
          return renderTmp(child, h)
        }
      })
    ) : h(
      d.tag,
      d.config
    )
  }
  export default {
    render(h) {
      let d = lodash.cloneDeep(this.tmp)
      return renderTmp(d, h)
    },
    data() {
      return {
        str: 'h1',
        tmp: {
          tag: 'div',
          tagId: 'div1',
          config: {
            domProps: {
              id: 'div1'
            },
            on: {
              click: function () {
                console.log('div1')
              }
            }
          },
          children: [
            {
              tag: 'el-row',
              tagId: '2.1',
              config: {
                props: {
                  type: 'flex',
                  justify: 'left'
                },
                domProps: {
                  id: 'el-row-2.1'
                }
              },
              children: [
                {
                  tag: 'el-col',
                  tagId: 'el-col-3.1',
                  config: {
                    props: {
                      span: 4
                    }
                  },
                  children: [
                    {
                      tag: 'el-row',
                      tagId: 'el-row-3.2',
                      config: null,
                      children: [
                        {
                          tag: 'button',
                          tagId: 'el-button-4.1',
                          config: {
                            props: {
                              type: 'primary',
                              dragable: true
                            },
                            domProps: {
                              dragable: true
                            },
                            on: {
                              dragstart (e) {
                                console.log('dragged')
                                e.dataTransfer.setData('cName', 'tal-table')
                                e.preventDefault()
                                e.stopPropagation()
                              },
                              click (e) {
                                console.log('table btn was clicked')
                                e.preventDefault()
                              }
                            }
                          },
                          children: ['表格']
                        }
                      ]
                    },
                    {
                      tag: 'el-row',
                      tagId: 'el-row-3.2',
                      config: {
                        class: ['mgtp10']
                      },
                      children: [
                        {
                          tag: 'el-button',
                          tagId: 'el-button-4.1',
                          config: {
                            props: {
                              type: 'primary'
                            },
                            domProps: {
                              dragable: true
                            },
                            on: {
                              dragstart (e) {
                                e.dataTransfer.setData('cName', 'el-input')
                                e.preventDefault()
                                e.stopPropagation()
                              },
                              click (e) {
                                console.log('table btn was clicked')
                                e.preventDefault()
                              }
                            }
                          },
                          children: ['输入框']
                        }
                      ]
                    }
                  ]
                },
                {
                  tag: 'el-col',
                  tagId: 'el-col-3.1',
                  config: null,
                  children: [
                    {
                      tag: 'div',
                      tagId: 'div-4.1',
                      config: {
                        style: {
                          border: '1px solid #000'
                        }
                      },
                      children: [
                        '这是一个工作区'
                      ]
                    }
                  ]
                }
              ]
            },
            {
              tag: 'div',
              tagId: '2.2',
              config: {
                domProps: {
                  id: 'p-2.2'
                },
                on: {
                  click() {
                    console.log('3')
                  }
                }
              },
              children: [{
                tag: 'span',
                config: {
                  domProps: {
                    id: 'span-3.1'
                  },
                  style: {
                    color: 'red',
                    fontSize: '14px'
                  },
                  on: {
                    click() {
                      console.log('3.1')
                    }
                  }
                },
                children: [
                  {
                    tag: 'em',
                    config: null,
                    children: ['这是p标签的内容，这是一大段文字，只有最愚蠢的人才会看到几个字~~~~~~~']
                  },
                  {
                    tag: 'el-input',
                    config: {
                      on: {
                        blur: this.kill
                      },
                      style: {
                        width: '100px'
                      }
                    }
                  }
                ]
              }]
            }
          ]
        },
        values: '1'
      }
    },
    methods: {
      kill() {
        console.log('focused')
      }
    },
    mounted() {
      setTimeout(() => {
        this.tmp.children.push({
          tag: 'h2',
          config: {
            domProps: {
              id: '1-h2'
            },
            style: {
              color: 'red',
              border: '1px solid #00b38a'
            },
            on: {
              click: (e) => {
                console.log('1-h2')
                e.stopPropagation()
              }
            }
          },
          children: ['这是另一个标题党']
        })
      }, 2000)
    }
  }
</script>

<style scoped>
  .mgtp10 {
    margin-top: 10px;
  }
</style>
