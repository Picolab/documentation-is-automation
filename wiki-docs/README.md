# Pointers on editing the Pico Labs documentation

## An internal link to another section of the same document

1. Right click on the anchor section heading, then choose Inspect
1. Observe the `id` for that heading (e.g., `ManagingSubscriptions-SubscriptionAttributes`). It will be the document name (munged together), a hyphen, and the internal `id` that we will need for the link
(See Figure 1.)
1. Go to where you want the link, highlighting the text of the link
1. Click on the Insert link widget 🔗
1. Choose Advanced for the type of link
1. Enter the internal `id` (the part _after_ the hypen, preceded by a number sign) as the Link (e.g., `#SubscriptionAttributes`)
(See Figure 2.)
1. Click on the Insert button

### Figure 1.

Showing the internal `id` of this section heading will be `SubscriptionAttributes`

![Figure 1](https://picolab.github.io/documentation-is-automation/wiki-docs/section_id.png)

### Figure 2.

![Figure 2](https://picolab.github.io/documentation-is-automation/wiki-docs/advanced_link.png)

